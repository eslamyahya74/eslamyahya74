function result = bernoulli_equation(h)
    % Given parameters
    Q = 1.2; % m^3/s
    ho = 0.6; % m
    H = 0.075; % m
    g = 9.81; % m/s^2
    b = 1.8; % m
    
    % Bernoulli's Equation
    result = Q^2 / (2 * g * b * h) + ho + h + H - Q^2 / (2 * g * b * ho);
end

function height = bisection_method(func, a, b, es, max_iter)
    % Bisection Method to find the root of a function within [a, b]
    % func: the function to find the root of
    % a, b: interval boundaries
    % es: desired relative error (stopping criterion)
    % max_iter: maximum number of iterations
    
    if func(a) * func(b) > 0
        error('Invalid interval; function must change sign within the interval.');
    end
    
    iter = 0;
    ea = inf;
    while ea > es && iter < max_iter
        c = (a + b) / 2;
        fc = func(c);
        
        if fc == 0
            break; % exact root found
        elseif func(a) * fc < 0
            b = c;
        else
            a = c;
        end
        
        if c ~= 0
            ea = abs((b - a) / c) * 100;
        end
        
        iter = iter + 1;
    end
    
    height = (a + b) / 2;
end

% Given parameters
initial_guess_a = 0.05;
initial_guess_b = 0.5;
es = 1e-7;
max_iter = 100;

% Solve using Bisection Method
result_height = bisection_method(@bernoulli_equation, initial_guess_a, initial_guess_b, es, max_iter);

% Display the result
fprintf('The height of water above the bump: %.5f meters\n', result_height);
