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

### QLF bound: NPA Hierarchy Level 1

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

### QLF bound: NPA Hierarchy Level 1+AB

```matlab

cvx_begin sdp

cvx_precision high
cvx_solver mosek

variable Q(16,16) semidefinite; % set up the moment matrix

variable v; % define the optimisation variable

% input the constraints

v == Q(1,1) + Q(2,2) + Q(3,3) + Q(4,4) + Q(5,5) + Q(6,6) + Q(7,7) + Q(8,8) + Q(9,9) + Q(10,10) + Q(11,11) + Q(12,12) + Q(13,13) + Q(14,14) + Q(15,15) + Q(16,16); % identity coefficients

1 == Q(7,4) + Q(8,5) + Q(9,6) + Q(16,1) + Q(4,7) + Q(5,8) + Q(6,9) + Q(1,16); % A1 coefficients
1 == Q(10,4) + Q(11,5) + Q(12,6) + Q(16,2) + Q(4,10) + Q(5,11) + Q(6,12) + Q(2,16); % A2 coefficients
1 == Q(7,1) + Q(10,2) + Q(13,3) + Q(16,4) + Q(1,7) + Q(2,10) + Q(3,13) + Q(4,16); % B1 coefficients
1 == Q(8,1) + Q(11,2) + Q(14,3) + Q(16,5) + Q(1,8) + Q(2,11) + Q(3,14) + Q(5,16); % B2 coefficients
1 == Q(5,1) + Q(1,5) + Q(16,8) + Q(8,16); % A1B2 coefficients
1 == Q(4,2) + Q(2,4) + Q(16,10) + Q(10,16); % A2B1 coefficients
-1 == Q(5,2) + Q(2,5) + Q(16,11) + Q(11,16); % A2B2 coefficients
1 == Q(6,2) + Q(2,6) + Q(16,12) + Q(12,16); % A2B3 coefficients
1 == Q(5,3) + Q(3,5) + Q(16,14) + Q(14,16); % A3B2 coefficients
1 == Q(6,3) + Q(3,6) + Q(16,15) + Q(15,16); % A3B3 coefficients

0 == Q(13,4) + Q(14,5) + Q(15,6) + Q(16,3) + Q(4,13) + Q(5,14) + Q(6,15) + Q(3,16); % A3
0 == Q(9,1) + Q(12,2) + Q(15,3) + Q(16,6) + Q(1,9) + Q(2,12) + Q(3,15) + Q(6,16); % B3

0 == Q(2,1) + Q(10,7) + Q(11,8) + Q(12,9); % A2A1
0 == Q(1,2) + Q(7,10) + Q(8,11) + Q(9,12); % A1A2
0 == Q(3,1) + Q(13,7) + Q(14,8) + Q(15,9); % A3A1
0 == Q(1,3) + Q(7,13) + Q(8,14) + Q(9,15); % A1A3
0 == Q(2,3) + Q(10,13) + Q(11,14) + Q(12,15); % A2A3
0 == Q(3,2) + Q(13,10) + Q(14,11) + Q(15,12); % A3A2

0 == Q(4,1) + Q(1,4) + Q(16,7) + Q(7,16); % A1B1
0 == Q(6,1) + Q(1,6) + Q(16,9) + Q(9,16); % A1B3
0 == Q(4,3) + Q(3,4) + Q(16,13) + Q(13,16); % A3B1

0 == Q(4,5) + Q(7,8) + Q(10,11) + Q(13,14); % B1B2
0 == Q(5,4) + Q(8,7) + Q(11,10) + Q(14,13); % B2B1
0 == Q(4,6) + Q(7,9) + Q(10,12) + Q(13,15); % B1B3
0 == Q(6,4) + Q(9,7) + Q(12,10) + Q(15,13); % B3B1
0 == Q(5,6) + Q(8,9) + Q(11,12) + Q(14,15); % B2B3
0 == Q(6,5) + Q(9,8) + Q(12,11) + Q(15,14); % B3B2

0 == Q(7,2) + Q(1,10); % A1A2B1
0 == Q(8,2) + Q(1,11); % A1A2B2
0 == Q(9,2) + Q(1,12); % A1A2B3
0 == Q(10,1) + Q(2,7); % A2A1B1
0 == Q(11,1) + Q(2,8); % A2A1B2
0 == Q(12,1) + Q(2,9); % A2A1B3
0 == Q(13,1) + Q(3,7); % A3A1B1
0 == Q(14,1) + Q(3,8); % A3A1B2
0 == Q(15,1) + Q(3,9); % A3A1B3
0 == Q(13,2) + Q(3,10); % A3A2B1
0 == Q(14,2) + Q(3,11); % A3A2B2
0 == Q(15,2) + Q(3,12); % A3A2B3
0 == Q(7,3) + Q(1,13); % A1A3B1
0 == Q(8,3) + Q(1,14); % A1A3B2
0 == Q(9,3) + Q(1,15); % A1A3B3
0 == Q(10,3) + Q(2,13); % A2A3B1
0 == Q(11,3) + Q(2,14); % A2A3B2
0 == Q(12,3) + Q(2,15); % A2A3B3
0 == Q(8,4) + Q(5,7); % A1B2B1
0 == Q(9,4) + Q(6,7); % A1B3B1
0 == Q(11,4) + Q(5,10); % A2B2B1
0 == Q(12,4) + Q(6,10); % A2B3B1
0 == Q(14,4) + Q(5,13); % A3B2B1
0 == Q(15,4) + Q(6,13); % A3B3B1
0 == Q(7,5) + Q(4,8); % A1B1B2
0 == Q(9,5) + Q(6,8); % A1B3B2
0 == Q(10,5) + Q(4,11); % A2B1B2
0 == Q(12,5) + Q(6,11); % A2B3B2
0 == Q(13,5) + Q(4,14); % A3B1B2
0 == Q(15,5) + Q(6,14); % A3B3B2
0 == Q(7,6) + Q(4,9); % A1B1B3
0 == Q(8,6) + Q(5,9); % A1B2B3
0 == Q(10,6) + Q(4,12); % A2B1B3
0 == Q(11,6) + Q(5,12); % A2B2B3
0 == Q(13,6) + Q(4,15); % A3B1B3
0 == Q(14,6) + Q(5,15); % A3B2B3

0 == Q(11,7);
0 == Q(12,7);
0 == Q(14,7);
0 == Q(15,7);
0 == Q(10,8);
0 == Q(12,8);
0 == Q(13,8);
0 == Q(15,8);
0 == Q(10,9);
0 == Q(11,9);
0 == Q(13,9);
0 == Q(14,9);
0 == Q(8,10);
0 == Q(9,10);
0 == Q(14,10);
0 == Q(15,10);
0 == Q(7,11);
0 == Q(9,11);
0 == Q(13,11);
0 == Q(15,11);
0 == Q(7,12);
0 == Q(8,12);
0 == Q(13,12);
0 == Q(14,12);
0 == Q(8,13);
0 == Q(9,13);
0 == Q(11,13);
0 == Q(12,13);
0 == Q(7,14);
0 == Q(9,14);
0 == Q(10,14);
0 == Q(12,14);
0 == Q(7,15);
0 == Q(8,15);
0 == Q(10,15);
0 == Q(11,15);


minimise v; % perform the optimisation
 
cvx_end

cvx_optval; % print the bound

[V,D] = eig(full(Q)) % find the eigenvectors V and corresponding eigenvalues D

chol(full(Q)) % find the Cholesky decomposition

```

## A new CGLMP-LF inequality

### Plotting figure 11.2

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

load NSvert.mat

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

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% DEFINING THE DECOMPOSITION ELEMENTS %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

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

M = delta + gamma;

vertices = zeros(2,1161*9);

for k = 1:1161*9
    vertices(1,k) = sum(sum(sum(sum(CGLMP.*F(:,:,:,:,k)))));
    vertices(2,k) = sum(sum(sum(sum(M.*F(:,:,:,:,k)))));
end

listsat = find([1 3]*vertices >= 4.99);

S = [];
for i = 2:length(listsat)
    S = [S; reshape(F(:,:,:,:,listsat(i)),1,[]) - reshape(F(:,:,:,:,listsat(1)),1,[])];
end

rank(S) % finding the rank of S (i.e. the vertex vectors as a matrix) is equivalent to finding the dimension of the corresponding face of the polytope

V = unique(vertices','rows')

k = convhull(V);
plot(V(:,1),V(:,2),'*')
hold on
plot(V(k,1),V(k,2))

% identifying the quantum region

n = 1001;
Mvec = linspace(-2,2,n);
CGLMPvec = zeros(1,n);

for i = 1:n
m = Mvec(i);

cvx_begin quiet
    variable P(3,3,3,3)
    maximise  sum(sum(sum(sum(CGLMP.*P))))
    subject to
    sum(sum(sum(sum(M.*P)))) == m;
    NPAHierarchy1(P,2) == 1;
cvx_end

CGLMPvec(i) = cvx_optval;
end

% plotting the boundary of the quantum set

plot(CGLMPvec,Mvec)

```

### Verifying the LF bound

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

load NSvert.mat

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

LF = CGLMP + 3*(delta + gamma); % defining LF as a sum of CGLMP, delta and gamma

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

CGLMPLF = CGLMP + 3*(delta + gamma); % defining LF as the sum of CGLMP, delta and gamma

%
% BellInequalityMax2(LF, [3,3,3,3], 'fp') % checking the local bound on LF (result = 3)

% checking the quantum bound on CGLMPLF (result = 3.69393 i.e. violation!)

   cvx_begin

       variable p(3,3,3,3)
         
       maximize(CGLMPLF(:)'*p(:))

       subject to

            NPAHierarchy1(p,2) == 1;
   cvx_end

```

### Finding the rank of the face

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

load NSvert.mat

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

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% DEFINING THE DECOMPOSITION ELEMENTS %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

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

M = delta + gamma;

vertices = zeros(2,1161*9);

for k = 1:1161*9
    vertices(1,k) = sum(sum(sum(sum(CGLMP.*F(:,:,:,:,k)))));
    vertices(2,k) = sum(sum(sum(sum(M.*F(:,:,:,:,k)))));
end

listsat = find([1 3]*vertices >= 4.99);

S = [];
for i = 2:length(listsat)
    S = [S; reshape(F(:,:,:,:,listsat(i)),1,[]) - reshape(F(:,:,:,:,listsat(1)),1,[])];
end

rank(S) % finding the rank of S (i.e. the vertex vectors as a matrix) is equivalent to finding the dimension of the corresponding face of the polytope

```

### Finding the maximally violating states and measurements

```matlab

% Finding the maximally violating states and measurements

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

CGLMPLF = CGLMP + 3*(delta + gamma); % defining LF as the sum of CGLMP, delta and gamma

psi = MaxEntangled(3);
rho = psi * psi';

A0 = RandomPOVM(3,3);
A1 = RandomPOVM(3,3);
A2 = RandomPOVM(3,3);

A = zeros(3,3,3,3);
A(:,:,1,1) = A0{1};
A(:,:,2,1) = A0{2};
A(:,:,3,1) = A0{3};
A(:,:,1,2) = A1{1};
A(:,:,2,2) = A1{2};
A(:,:,3,2) = A1{3};
A(:,:,1,3) = A2{1};
A(:,:,2,3) = A2{2};
A(:,:,3,3) = A2{3};

diff = 1;

while diff >= 1E-7

cvx_begin quiet

    variable B(3,3,3,3) complex

    expression beta1
    
    beta1 = 0;

    for a = 1:3
        for b = 1:3
            for x = 1:3
                for y = 1:3
                    beta1 = beta1 + CGLMPLF(a,b,x,y)*real(trace(rho*Tensor(A(:,:,a,x),B(:,:,b,y))));
                end
            end
        end
    end

    maximise beta1
    
    for y = 1:3
        for b = 1:3
            B(:,:,b,y) == hermitian_semidefinite(3)
        end
        B(:,:,1,y) + B(:,:,2,y) + B(:,:,3,y) == eye(3)
    end

cvx_end

cvx_begin quiet

    variable A(3,3,3,3) complex

    expression beta2
    
    beta2 = 0;

    for a = 1:3
        for b = 1:3
            for x = 1:3
                for y = 1:3
                    beta2 = beta2 + CGLMPLF(a,b,x,y)*real(trace(rho*Tensor(A(:,:,a,x),B(:,:,b,y))));
                end
            end
        end
    end

    maximise beta2
    
    for x = 1:3
        for a = 1:3
            A(:,:,a,x) == hermitian_semidefinite(3)
        end
        A(:,:,1,x) + A(:,:,2,x) + A(:,:,3,x) == eye(3)
    end

cvx_end

cvx_begin quiet

    variable rho(9,9) hermitian semidefinite

    expression beta3
    
    beta3 = 0;

    for a = 1:3
        for b = 1:3
            for x = 1:3
                for y = 1:3
                    beta3 = beta3 + CGLMPLF(a,b,x,y)*real(trace(rho*Tensor(A(:,:,a,x),B(:,:,b,y))));
                end
            end
        end
    end

    maximise beta3
    
    trace(rho) == 1

cvx_end

diff = beta3 - beta1;
[beta1 beta2 beta3 diff]

end

```