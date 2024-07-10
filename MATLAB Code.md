---
subject: Appendix B
subtitle:
short_title: MATLAB Code
numbering: 
    enumerator: B.%s
---

# MATLAB Code

## Figures ? and ?

MATLAB was used to calculate the quantum region and locate maximal quantum violations of the LF inequality (both overall and in the region identified as interesting). Vertices of the LF polytope were calculated by hand (see section ?) and therefore plotted manually. Note that the final appearance of figures ? and ? is slightly different from the output of this code. Firstly, the plot has been split into two separate graphs, each with fewer features, to emphasise different aspects. Secondly, details such as colour and line style have been edited to improve clarity. All changes were performed using the vector graphics software Adobe Illustrator.

```matlab
    
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% DEFINING THE FULL LF INEQUALITY %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% LF = M - 2*CHSH;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% DEFINING THE DECOMPOSITION ELEMENTS %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

M = zeros(2,2,3,3); 
M(2,2,1,1) = 1;
M(1,2,3,2) = 1;
M(2,1,2,3) = 1;
M(1,1,3,3) = -1;

CHSH = zeros(2,2,3,3); 
CHSH(1,1,1,1) = 1;
CHSH(2,1,2,1) = -1;
CHSH(1,2,1,2) = -1;
CHSH(1,1,2,2) = -1;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% PLOTTING A GRAPH IN THE NEW PARAMETER SPACE %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% identifying the quantum region

n = 10001;
Mvec = linspace(-1,2,n);
CHSHvec = zeros(1,n);

for i = 1:n
m = Mvec(i);

cvx_begin 
    variable P(2,2,3,3)
    minimise  sum(sum(sum(sum(CHSH.*P))))
    subject to
    sum(sum(sum(sum(M.*P)))) == m;
    NPAHierarchy(P,2) == 1;
cvx_end

CHSHvec(i) = cvx_optval;
end

% plotting the boundary of the quantum set
plot(CHSHvec,Mvec) 

hold on % this allows multiple features to be plotted on the same graph

% plotting a tangent to the quantum set (i.e. a possible QLF inequality) 
% in the region identified as interesting
xfit = -2 : 0.01 : 0.5 ; 
m = 1;
b = 2.2071;
yfit = m*xfit + b;
plot(xfit, yfit)

% plotting vertices of the LF polytope
plot(-1/2,2,'.') % point A
plot(0,2,'.') % point B
plot(0,-1,'.') % point C
plot(-1,-1,'.') % point D
plot(-1,1,'.') % point E

% plotting facets of the LF polytope
plot([-1/2,0],[2,2]) % line AB
plot([0,0],[2,-1]) % line BC
plot([0,-1],[-1,-1]) % line CD
plot([-1,-1],[-1,1]) % line DE
% line EA
x1 = -1 : 0.1 : -1/2 ;
m = 2;
b = 3;
y1 = m*x1 + b;
plot(x1,y1)

% plotting hyperplanes associated with relevant facets of the LF polytope
plot([-1.5,-0.5],[2,2]) % extending line AB to the left
plot([0,0.5],[2,2]) % extending line AB to the right
plot([-1,-1],[1,2.5]) % extending line DE below
plot([-1,-1],[-1.5,-1]) % extending line DE above
% extending line EA below and to the left
x2 = -1.5 : 0.1 : -1 ;
m = 2;
b = 3;
y2 = m*x2 + b;
plot(x2,y2)
% extending line EA above and to the right
x3 = -0.5 : 0.05 : -0.25 ;
m = 2;
b = 3;
y3 = m*x3 + b;
plot(x3,y3)

% plotting the overall maximal quantum violation of the LF inequality
plot(-1.1802,0.9758,`ok') 

% plotting the maximal quantum violation of the LF inequality
% in the region identified as interesting
plot(-1,1.2071,`ok') 

% setting up appropriate axes
xlabel(`CHSH')
ylabel(`M')
grid on
axis equal
axis([-1.5  0.5  -1.5  2.5])

hold off

```
## SOS decompositions of QLF

### Order of operators 1
### Order of operators 2
### Order of operators 3
### Order of operators 4
### Order of operators 5