# CFD
clc
clear 
close all



domain1 = 1;
n_points= 120;
h = domain1/ (n_points-1);
%%Initializing

y1(n_points,n_points) = 0;
y1(1,:) = 1;
y1_new(n_points,n_points) = 0;
y1_new(1,:) = 1;
err_mag = 1;
err_req = 1e-6;
iterations = 0;
%%Calculation
while err_mag > err_req

    for i = 2: (n_points-1)
        for j = 2: (n_points-1)

            y1_new(i,j) = 0.25*( y1(i+1,j)+ y1(i-1,j)+ y1(i,j+1)+ y1(i,j-1));

            iterations = iterations+1;

        end
    end
   
%%solve for err_mag
err_mag= 0;
    for i = 2: (n_points-1)
        for j = 2: (n_points-1)
            err_mag = err_mag + abs(y1_new(i,j)-y1(i,j));
        end
    end

y1 = y1_new;
end


x1_dom1 = ((1:n_points)-1)*h;
y1_dom1 = 1-((1:n_points)-1)*h;

[X1,Y1] = meshgrid(x1_dom1, y1_dom1);

contourf(X1,Y1,y1,25);  
colorbar
