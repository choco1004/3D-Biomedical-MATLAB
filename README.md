# 3D-Biomedical-MATLAB
3D Biomedical Data Visualization using MATLAB
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
