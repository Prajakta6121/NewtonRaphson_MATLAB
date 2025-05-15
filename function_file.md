# NewtonRaphson_MATLAB
Write a code in MATLAB to find the roots of the given function using NEWTON - RAPHSON Method
function [root, iterations] = newtonraphson(f, df, x0)
% NEWTONRAPHSON Implements the Newton-Raphson method for root finding
% Inputs:
%   f  - Function handle
%   df - Derivative of the function handle
%   x0 - Initial guess
% Outputs:
%   root - Estimated root
%   iterations - Number of iterations taken

% Convergence criteria and maximum iterations
delta = 0.001;
maxIter = 100;
iterations = 1;

% Print header
fprintf('Iteration no.   Lowerbound(a)   Upperbound(b)   New estimate(x)\n');
fprintf('_____________________________________________________________\n');

while iterations <= maxIter
    fx = f(x0);           % Evaluate function
    dfx = df(x0);         % Evaluate derivative

    if dfx == 0
        fprintf('\nDerivative zero. Choose another starting point.\n');
        break;
    end

    x1 = x0 - fx/dfx;     % Newton-Raphson update formula
    absErr = abs(x1 - x0);
    relErr = absErr / (abs(x1) + eps);

    % Print iteration info
    fprintf('%7d %18s %18s %22.4f\n', iterations, '-', '-', x1);

    if absErr < delta && relErr < delta
        break;
    end

    x0 = x1;
    iterations = iterations + 1;
end

root = x1;
end
