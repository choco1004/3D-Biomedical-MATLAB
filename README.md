# 3D-Biomedical-MATLAB
3D Biomedical Data Visualization using MATLAB

https://drive.mathworks.com/sharing/4bed6a32-9ec0-4a25-9ff8-3bef3acf135d/PK%20%EB%AA%A8%EB%8D%B8%20+%20%EC%8B%9C%EA%B0%81%ED%99%94.m

clc;
clear;
close all;

%% =========================
% 1. PK MODEL (Time vs Concentration)
% ==========================

t = linspace(0, 24, 100);   % 시간 (hours)

D = 500;    % Dose (mg)
V = 50;     % Volume (L)
k = 0.2;    % Elimination rate constant

C = (D/V) * exp(-k * t);

figure;
plot(t, C, 'LineWidth', 2);
xlabel('Time (hours)');
ylabel('Concentration (mg/L)');
title('Drug Concentration over Time');
grid on;

%% =========================
% 2. 3D Drug Diffusion Model
% ==========================

depth = linspace(0, 10, 50);   % 조직 깊이
[T, Dp] = meshgrid(t, depth);

% 농도 모델 (시간 감소 + 깊이 감쇠)
C3D = (D/V) .* exp(-k .* T) .* exp(-0.1 .* Dp);

figure;
surf(T, Dp, C3D);

xlabel('Time');
ylabel('Tissue Depth');
zlabel('Concentration');

title('3D Drug Diffusion Simulation');

colorbar;
shading interp;
view(45, 30);
