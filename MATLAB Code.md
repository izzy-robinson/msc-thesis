---
subject: Appendix B
subtitle:
short_title: MATLAB Code
numbering: 
    enumerator: B.%s
---

# MATLAB Code

## Figures 9.6 and 10.1

MATLAB was used to calculate the quantum region and locate maximal quantum violations of the LF inequality (both overall and in the region identified as interesting). Vertices of the LF polytope were calculated by hand and therefore plotted manually. Note that the final appearance of figures [](#LF-graph-figure) and [](#QLF-graph-figure) is slightly different from the output of this code. Firstly, the plot has been split into two separate graphs, each with fewer features, to emphasise different aspects. Secondly, details such as colour and line style have been edited to improve clarity. All changes were performed using the vector graphics software Adobe Illustrator.

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

## SOS decompositions 

### CHSH bound

```matlab

cvx_begin sdp

cvx_precision high

variable Q(5,5) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5); % identity coefficients

0 == Q(1,2) + Q(2,1); % A1 coefficient
0 == Q(1,3) + Q(3,1); % A2 coefficients

0 == Q(1,4) + Q(4,1); % B1 coefficients
0 == Q(1,5) + Q(5,1); % B2 coefficients

0 == Q(2,3); % A1B1 coefficients
0 == Q(3,2); % A1B2 coefficients
0 == Q(4,5); % A2B1 coefficients
0 == Q(5,4); % A2B2 coefficients

-1 == Q(2,4) + Q(4,2); % A1A2 coefficients
-1 == Q(2,5) + Q(5,2); % A2A1 coefficients

-1 == Q(3,4) + Q(4,3); % B1B2 coefficients
1 == Q(3,5) + Q(5,3); % B2B1 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

### QLF bound: Order of operators 1

```matlab

cvx_begin sdp

cvx_precision high

variable Q(7,7) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7); % identity coefficients

1 == Q(1,2) + Q(2,1); % A1 coefficients
1 == Q(1,3) + Q(3,1); % A2 coefficients
0 == Q(1,4) + Q(4,1); % A3 coefficients

1 == Q(1,5) + Q(5,1); % B1 coefficients
1 == Q(1,6) + Q(6,1); % B2 coefficients
0 == Q(1,7) + Q(7,1); % B3 coefficients

0 == Q(2,5) + Q(5,2); % A1B1 coefficients
1 == Q(2,6) + Q(6,2); % A1B2 coefficients
0 == Q(2,7) + Q(7,2); % A1B3 coefficients
1 == Q(3,5) + Q(5,3); % A2B1 coefficients
-1 == Q(3,6) + Q(6,3); % A2B2 coefficients
1 == Q(3,7) + Q(7,3); % A2B3 coefficients
0 == Q(4,5) + Q(5,4); % A3B1 coefficients
1 == Q(4,6) + Q(6,4); % A3B2 coefficients
1 == Q(4,7) + Q(7,4); % A3B3 coefficients

0 == Q(2,3); % A1A2 coefficients
0 == Q(3,2); % A2A1 coefficients
0 == Q(2,4); % A1A3 coefficients
0 == Q(4,2); % A3A1 coefficients
0 == Q(3,4); % A2A3 coefficients
0 == Q(4,3); % A3A2 coefficients

0 == Q(5,6); % B1B2 coefficients
0 == Q(6,5); % B2B1 coefficients
0 == Q(5,7); % B1B3 coefficients
0 == Q(7,5); % B3B1 coefficients
0 == Q(6,7); % B2B3 coefficients
0 == Q(7,6); % B3B2 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

### QLF bound: Order of operators 2

```matlab

cvx_begin sdp

cvx_precision high

variable Q(7,7) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7); % identity coefficients

1 == Q(1,7) + Q(7,1); % A1 coefficients
1 == Q(2,7) + Q(7,2); % A2 coefficients
0 == Q(3,7) + Q(7,3); % A3 coefficients

1 == Q(4,7) + Q(7,4); % B1 coefficients
1 == Q(5,7) + Q(7,5); % B2 coefficients
0 == Q(6,7) + Q(7,6); % B3 coefficients

0 == Q(1,4) + Q(4,1); % A1B1 coefficients
1 == Q(1,5) + Q(5,1); % A1B2 coefficients
0 == Q(1,6) + Q(6,1); % A1B3 coefficients
1 == Q(2,4) + Q(4,2); % A2B1 coefficients
-1 == Q(2,5) + Q(5,2); % A2B2 coefficients
1 == Q(2,6) + Q(6,2); % A2B3 coefficients
0 == Q(3,4) + Q(4,3); % A3B1 coefficients
1 == Q(3,5) + Q(5,3); % A3B2 coefficients
1 == Q(3,6) + Q(6,3); % A3B3 coefficients

0 == Q(1,2); % A1A2 coefficients
0 == Q(2,1); % A2A1 coefficients
0 == Q(1,3); % A1A3 coefficients
0 == Q(3,1); % A3A1 coefficients
0 == Q(2,3); % A2A3 coefficients
0 == Q(3,2); % A3A2 coefficients

0 == Q(4,5); % B1B2 coefficients
0 == Q(5,4); % B2B1 coefficients
0 == Q(4,6); % B1B3 coefficients
0 == Q(6,4); % B3B1 coefficients
0 == Q(5,6); % B2B3 coefficients
0 == Q(6,4); % B3B2 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

### QLF bound: Order of operators 3

```matlab

cvx_begin sdp

cvx_precision high

variable Q(7,7) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7); % identity coefficients

1 == Q(1,2) + Q(2,1); % A1 coefficients
1 == Q(1,3) + Q(3,1); % B1 coefficients

1 == Q(1,4) + Q(4,1); % A2 coefficients
1 == Q(1,5) + Q(5,1); % B2 coefficients

0 == Q(1,6) + Q(6,1); % A3 coefficients
0 == Q(1,7) + Q(7,1); % B3 coefficients

0 == Q(2,3) + Q(3,2); % A1B1 coefficients
1 == Q(2,5) + Q(5,2); % A1B2 coefficients
0 == Q(2,7) + Q(7,2); % A1B3 coefficients
1 == Q(3,4) + Q(4,3); % A2B1 coefficients
-1 == Q(4,5) + Q(5,4); % A2B2 coefficients
1 == Q(4,7) + Q(7,4); % A2B3 coefficients
0 == Q(3,6) + Q(6,3); % A3B1 coefficients
1 == Q(5,6) + Q(6,5); % A3B2 coefficients
1 == Q(6,7) + Q(7,6); % A3B3 coefficients

0 == Q(2,4); % A1A2 coefficients
0 == Q(4,2); % A2A1 coefficients
0 == Q(2,6); % A1A3 coefficients
0 == Q(6,2); % A3A1 coefficients
0 == Q(4,6); % A2A3 coefficients
0 == Q(6,4); % A3A2 coefficients

0 == Q(3,5); % B1B2 coefficients
0 == Q(5,3); % B2B1 coefficients
0 == Q(3,7); % B1B3 coefficients
0 == Q(7,3); % B3B1 coefficients
0 == Q(5,7); % B2B3 coefficients
0 == Q(7,5); % B3B2 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

### QLF bound: Order of operators 4

```matlab

cvx_begin sdp

cvx_precision high

variable Q(7,7) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7); % identity coefficients

1 == Q(1,7) + Q(7,1); % A1 coefficients
1 == Q(2,7) + Q(7,2); % B1 coefficients

1 == Q(3,7) + Q(7,3); % A2 coefficients
1 == Q(4,7) + Q(7,4); % B2 coefficients

0 == Q(5,7) + Q(7,5); % A3 coefficients
0 == Q(6,7) + Q(7,6); % B3 coefficients

0 == Q(1,2) + Q(2,1); % A1B1 coefficients
1 == Q(1,4) + Q(4,1); % A1B2 coefficients
0 == Q(1,6) + Q(6,1); % A1B3 coefficients
1 == Q(2,3) + Q(3,2); % A2B1 coefficients
-1 == Q(3,4) + Q(4,3); % A2B2 coefficients
1 == Q(3,6) + Q(6,3); % A2B3 coefficients
0 == Q(2,5) + Q(5,2); % A3B1 coefficients
1 == Q(4,5) + Q(5,4); % A3B2 coefficients
1 == Q(5,6) + Q(6,5); % A3B3 coefficients

0 == Q(1,3); % A1A2 coefficients
0 == Q(3,1); % A2A1 coefficients
0 == Q(1,5); % A1A3 coefficients
0 == Q(5,1); % A3A1 coefficients
0 == Q(3,5); % A2A3 coefficients
0 == Q(5,3); % A3A2 coefficients

0 == Q(2,4); % B1B2 coefficients
0 == Q(4,2); % B2B1 coefficients
0 == Q(2,6); % B1B3 coefficients
0 == Q(6,2); % B3B1 coefficients
0 == Q(4,6); % B2B3 coefficients
0 == Q(6,4); % B3B2 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

### QLF bound: Order of operators 5

```matlab

cvx_begin sdp

cvx_precision high

variable Q(7,7) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7); % identity coefficients

1 == Q(4,5) + Q(5,4); % A1 coefficient
1 == Q(3,5) + Q(5,3); % A2 coefficients
0 == Q(5,7) + Q(7,5); % A3 coefficients

1 == Q(2,5) + Q(5,2); % B1 coefficients
1 == Q(5,6) + Q(6,5); % B2 coefficients
0 == Q(1,5) + Q(5,1); % B3 coefficients

0 == Q(2,4) + Q(4,2); % A1B1 coefficients
1 == Q(4,6) + Q(6,4); % A1B2 coefficients
0 == Q(1,4) + Q(4,1); % A1B3 coefficients
1 == Q(2,3) + Q(3,2); % A2B1 coefficients
-1 == Q(3,6) + Q(6,3); % A2B2 coefficients
1 == Q(1,3) + Q(3,1); % A2B3 coefficients
0 == Q(2,7) + Q(7,2); % A3B1 coefficients
1 == Q(6,7) + Q(7,6); % A3B2 coefficients
1 == Q(1,7) + Q(7,1); % A3B3 coefficients

0 == Q(4,3); % A1A2 coefficients
0 == Q(3,4); % A2A1 coefficients
0 == Q(4,7); % A1A3 coefficients
0 == Q(7,4); % A3A1 coefficients
0 == Q(3,7); % A2A3 coefficients
0 == Q(7,3); % A3A2 coefficients

0 == Q(2,6); % B1B2 coefficients
0 == Q(6,2); % B2B1 coefficients
0 == Q(2,1); % B1B3 coefficients
0 == Q(1,2); % B3B1 coefficients
0 == Q(6,1); % B2B3 coefficients
0 == Q(1,6); % B3B2 coefficients

minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

## A new CGLMP-LF inequality

### Finding the LF bound

```matlab

r1 = zeros(3,3,2,2);
r1(1,1,1,1) = 1;
R1 = fp2cg(r1);

r2 = zeros(3,3,2,2);
r2(2,1,1,1) = 1;
R2 = fp2cg(r2);

r3 = zeros(3,3,2,2);
r3(3,1,1,1) = 1;
R3 = fp2cg(r3);

r4 = zeros(3,3,2,2);
r4(1,2,1,1) = 1;
R4 = fp2cg(r4);

r5 = zeros(3,3,2,2);
r5(2,2,1,1) = 1;
R5 = fp2cg(r5);

r6 = zeros(3,3,2,2);
r6(3,2,1,1) = 1;
R6 = fp2cg(r6);

r7 = zeros(3,3,2,2);
r7(1,3,1,1) = 1;
R7 = fp2cg(r7);

r8 = zeros(3,3,2,2);
r8(2,3,1,1) = 1;
R8 = fp2cg(r8);

r9 = zeros(3,3,2,2);
r9(3,3,1,1) = 1;
R9 = fp2cg(r9);

%%%%%%%%%%%%%%%%%%%

r10 = zeros(3,3,2,2);
r10(1,1,2,1) = 1;
R10 = fp2cg(r10);

r11 = zeros(3,3,2,2);
r11(2,1,2,1) = 1;
R11 = fp2cg(r11);

r12 = zeros(3,3,2,2);
r12(3,1,2,1) = 1;
R12 = fp2cg(r12);

r13 = zeros(3,3,2,2);
r13(1,2,2,1) = 1;
R13 = fp2cg(r13);

r14 = zeros(3,3,2,2);
r14(2,2,2,1) = 1;
R14 = fp2cg(r14);

r15 = zeros(3,3,2,2);
r15(3,2,2,1) = 1;
R15 = fp2cg(r15);

r16 = zeros(3,3,2,2);
r16(1,3,2,1) = 1;
R16 = fp2cg(r16);

r17 = zeros(3,3,2,2);
r17(2,3,2,1) = 1;
R17 = fp2cg(r17);

r18 = zeros(3,3,2,2);
r18(3,3,2,1) = 1;
R18 = fp2cg(r18);

%%%%%%%%%%%%%%%%%%%

r19 = zeros(3,3,2,2);
r19(1,1,1,2) = 1;
R19 = fp2cg(r19);

r20 = zeros(3,3,2,2);
r20(2,1,1,2) = 1;
R20 = fp2cg(r20);

r21 = zeros(3,3,2,2);
r21(3,1,1,2) = 1;
R21 = fp2cg(r21);

r22 = zeros(3,3,2,2);
r22(1,2,1,2) = 1;
R22 = fp2cg(r22);

r23 = zeros(3,3,2,2);
r23(2,2,1,2) = 1;
R23 = fp2cg(r23);

r24 = zeros(3,3,2,2);
r24(3,2,1,2) = 1;
R24 = fp2cg(r24);

r25 = zeros(3,3,2,2);
r25(1,3,1,2) = 1;
R25 = fp2cg(r25);

r26 = zeros(3,3,2,2);
r26(2,3,1,2) = 1;
R26 = fp2cg(r26);

r27 = zeros(3,3,2,2);
r27(3,3,1,2) = 1;
R27 = fp2cg(r27);

%%%%%%%%%%%%%%%%%%%

r28 = zeros(3,3,2,2);
r28(1,1,2,2) = 1;
R28 = fp2cg(r28);

r29 = zeros(3,3,2,2);
r29(2,1,2,2) = 1;
R29 = fp2cg(r29);

r30 = zeros(3,3,2,2);
r30(3,1,2,2) = 1;
R30 = fp2cg(r30);

r31 = zeros(3,3,2,2);
r31(1,2,2,2) = 1;
R31 = fp2cg(r31);

r32 = zeros(3,3,2,2);
r32(2,2,2,2) = 1;
R32 = fp2cg(r32);

r33 = zeros(3,3,2,2);
r33(3,2,2,2) = 1;
R33 = fp2cg(r33);

r34 = zeros(3,3,2,2);
r34(1,3,2,2) = 1;
R34 = fp2cg(r34);

r35 = zeros(3,3,2,2);
r35(2,3,2,2) = 1;
R35 = fp2cg(r35);

r36 = zeros(3,3,2,2);
r36(3,3,2,2) = 1;
R36 = fp2cg(r36);

%%%%%%%%%%%%%%%%%%%

R = [ R1(:)' ; R2(:)' ; R3(:)' ; R4(:)' ; R5(:)' ; R6(:)' ; R7(:)' ; R8(:)' ; R9(:)' ;
    R10(:)' ; R11(:)' ; R12(:)' ; R13(:)' ; R14(:)' ; R15(:)' ; R16(:)' ; R17(:)' ; R18(:)' ;
    R19(:)' ; R20(:)' ; R21(:)' ; R22(:)' ; R23(:)' ; R24(:)' ; R25(:)' ; R26(:)' ; R27(:)' ;
    R28(:)' ; R29(:)' ; R30(:)' ; R31(:)' ; R32(:)' ; R33(:)' ; R34(:)' ; R35(:)' ; R36(:)' ];

% We can split this matrix R into two, giving constraints in the form Ax >= b (i.e. b-Ax >= 0)

A = R(:, 2:25);

b = R(:,1);

% But the full matrix R is exactly what LRS wants as an input

% The following line sends from matlab to LRS
% dlmwrite('test.txt',R,'delimiter',' ');

% The following line sends from LRS to matlab

C = readmatrix('C:\Users\entan\AppData\Local\Microsoft\Attachments\vertices.txt');

% Reshape each of the 1161 rows of C (composed of 25 numbers) into 5x5 grids
% cg2fp each 'row'

D = zeros(5,5,1161);
E = zeros(3,3,2,2,1161);

for k = 1:1161 % Iterating over k with an initial value of 1, step value of 1, final value of 1161
    D(:,:,k) = reshape(C(k,:),[5,5]);
    E(:,:,:,:,k) = cg2fp(D(:,:,k),[3,3,2,2],1);
end

% The top left number is always 1 to indicate each is a vertex
% (as opposed to an array which would have top left number 0)



% add settings to turn each 'row'  into 9 full grids

F = zeros(3,3,3,3,1161*9);
counter = 1;

for k = 1:1:1161
    for a_0 = 1:3
        for b_0 = 1:3
            F(a_0,b_0,1,1,counter) = 1;
            F(:,b_0,2:3,1,counter) = sum(E(:,:,:,2,k),2);
            F(a_0,:,1,2:3,counter) = sum(E(:,:,2,:,k),1);
            F(:,:,2:3,2:3,counter) = E(:,:,:,:,k);
            counter = counter + 1;
        end
    end
end

CGLMP = zeros(3,3,3,3); % setting up the CGLMP grid

CGLMP(1,1,1,1) = +1;
CGLMP(3,1,1,1) = -1;
CGLMP(1,2,1,1) = -1;
CGLMP(2,2,1,1) = +1;
CGLMP(2,3,1,1) = -1;
CGLMP(3,3,1,1) = +1;

CGLMP(1,1,2,1) = +1;
CGLMP(2,1,2,1) = -1;
CGLMP(2,2,2,1) = +1;
CGLMP(3,2,2,1) = -1;
CGLMP(1,3,2,1) = -1;
CGLMP(3,3,2,1) = +1;

CGLMP(1,1,1,2) = +1;
CGLMP(2,1,1,2) = -1;
CGLMP(2,2,1,2) = +1;
CGLMP(3,2,1,2) = -1;
CGLMP(1,3,1,2) = -1;
CGLMP(3,3,1,2) = +1;

CGLMP(1,1,2,2) = -1;
CGLMP(2,1,2,2) = +1;
CGLMP(2,2,2,2) = -1;
CGLMP(3,2,2,2) = +1;
CGLMP(1,3,2,2) = +1;
CGLMP(3,3,2,2) = -1;

delta = zeros(3,3,3,3); % setting up the delta grid

delta(3,1,1,1) = +1;

gamma = zeros(3,3,3,3); % setting up the gamma grid

gamma(2,1,3,2) = -1;
gamma(1,2,3,2) = +1;
gamma(2,1,2,3) = +1;
gamma(3,2,2,3) = -1;
gamma(1,1,3,3) = -1;

LF = CGLMP + delta + gamma; % defining LF as the sum of CGLMP, delta and gamma

violations = zeros(1,1161*9);

for k = 1:1:1161*9
    temp = F(:,:,:,:,k);
    violations(1,k) = LF(:)'*temp(:);
end

max(violations);
sum(violations==3);
sum(violations>=2.99);
[i,j] = max(violations);

J = violations(find(violations == max(violations)));
L = zeros(length(J),81);

for k = 1:1:length(J)
    L(k,:) = reshape(F(:,:,:,:,k),1,[]);
end

max(violations)
rank(L)

```

### Finding the quantum maximum

```matlab

CGLMP = zeros(3,3,3,3); % setting up the CGLMP grid

CGLMP(1,1,1,1) = +1;
CGLMP(3,1,1,1) = -1;
CGLMP(1,2,1,1) = -1;
CGLMP(2,2,1,1) = +1;
CGLMP(2,3,1,1) = -1;
CGLMP(3,3,1,1) = +1;

CGLMP(1,1,2,1) = +1;
CGLMP(2,1,2,1) = -1;
CGLMP(2,2,2,1) = +1;
CGLMP(3,2,2,1) = -1;
CGLMP(1,3,2,1) = -1;
CGLMP(3,3,2,1) = +1;

CGLMP(1,1,1,2) = +1;
CGLMP(2,1,1,2) = -1;
CGLMP(2,2,1,2) = +1;
CGLMP(3,2,1,2) = -1;
CGLMP(1,3,1,2) = -1;
CGLMP(3,3,1,2) = +1;

CGLMP(1,1,2,2) = -1;
CGLMP(2,1,2,2) = +1;
CGLMP(2,2,2,2) = -1;
CGLMP(3,2,2,2) = +1;
CGLMP(1,3,2,2) = +1;
CGLMP(3,3,2,2) = -1;

delta = zeros(3,3,3,3); % setting up the delta grid

delta(3,1,1,1) = +1;

gamma = zeros(3,3,3,3); % setting up the gamma grid

gamma(2,1,3,2) = -1;
gamma(1,2,3,2) = +1;
gamma(2,1,2,3) = +1;
gamma(3,2,2,3) = -1;
gamma(1,1,3,3) = -1;

CGLMPLF = CGLMP + delta + gamma; % defining LF as the sum of CGLMP, delta and gamma

%
% BellInequalityMax2(LF, [3,3,3,3], 'fp') % checking the local bound on LF (result = 3)

% checking the quantum bound on CGLMPLF (result = 3.69393 i.e. violation!)

   cvx_begin

       variable p(3,3,3,3)
         
       maximize(CGLMPLF(:)'*p(:))

       subject to

            NPAHierarchy(p,2) == 1;
   cvx_end

```

### Finding the maximally violating states and measurements

```matlab

```