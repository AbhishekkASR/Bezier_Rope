Interactive Bézier Curve with Spring Physics
Overview

This project implements an interactive cubic Bézier curve that behaves like a flexible rope.
The curve responds in real time to user input (mouse movement) and visualizes both the curve geometry and its tangents. All mathematics, physics, and rendering logic are implemented manually without using any prebuilt Bézier or physics libraries.

Mathematical Model
Cubic Bézier Curve

The curve is defined using four control points:

P₀, P₃ → fixed endpoints

P₁, P₂ → dynamic control points

For a parameter 
𝑡
∈
[
0
,
1
]
t∈[0,1], the curve is evaluated as:

𝐵
(
𝑡
)
=
(
1
−
𝑡
)
3
𝑃
0
+
3
(
1
−
𝑡
)
2
𝑡
𝑃
1
+
3
(
1
−
𝑡
)
𝑡
2
𝑃
2
+
𝑡
3
𝑃
3
B(t)=(1−t)
3
P
0
	​

+3(1−t)
2
tP
1
	​

+3(1−t)t
2
P
2
	​

+t
3
P
3
	​


The curve is rendered by sampling 
𝑡
t at small intervals (Δt = 0.01) and drawing a polyline through the evaluated points.

Tangent Computation

Tangents are computed using the analytical derivative of the cubic Bézier equation:

𝐵
′
(
𝑡
)
=
3
(
1
−
𝑡
)
2
(
𝑃
1
−
𝑃
0
)
+
6
(
1
−
𝑡
)
𝑡
(
𝑃
2
−
𝑃
1
)
+
3
𝑡
2
(
𝑃
3
−
𝑃
2
)
B
′
(t)=3(1−t)
2
(P
1
	​

−P
0
	​

)+6(1−t)t(P
2
	​

−P
1
	​

)+3t
2
(P
3
	​

−P
2
	​

)

The resulting vector is normalized and drawn as a short line segment at selected points along the curve to visualize direction and curvature.

Physics Model
Spring–Damping System

The dynamic control points (P₁ and P₂) follow a mass–spring–damper model to achieve smooth, rope-like motion.

The acceleration is computed as:

𝑎
=
−
𝑘
(
𝑥
−
𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
)
−
𝑐
𝑣
a=−k(x−x
target
	​

)−cv

Where:

𝑘
k is the spring stiffness

𝑐
c is the damping coefficient

𝑣
v is the velocity

𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
x
target
	​

 is the position derived from user input

Velocity and position are updated using explicit Euler integration:

𝑣
←
𝑣
+
𝑎
⋅
𝑑
𝑡
v←v+a⋅dt
𝑥
←
𝑥
+
𝑣
⋅
𝑑
𝑡
x←x+v⋅dt

This approach provides natural lag, elasticity, and stability without external physics engines.

Interaction Design

Mouse movement defines target positions for the dynamic control points.
Instead of snapping directly to the mouse, the targets are blended with the current positions to maintain smooth motion and prevent instability. This indirect control produces the visual effect of a flexible rope being influenced rather than rigidly dragged.

Rendering Pipeline

Each animation frame performs the following steps:

Update physics for P₁ and P₂

Sample the Bézier curve

Draw the curve path

Draw tangent vectors

Draw control points

Rendering is performed using the HTML Canvas API with requestAnimationFrame, maintaining approximately 60 FPS.

Design Choices

Manual Bézier math ensures full mathematical transparency

Spring-damping physics provides realistic motion with minimal complexity

Fixed endpoints simplify constraints and improve visual clarity

Normalized tangents make direction visualization consistent

No external libraries to comply with assignment constraints

Performance Considerations

Curve sampling is limited to ~100 points per frame

Physics updates are constant-time

Canvas redraws are lightweight and stable at real-time frame rates

Conclusion

This implementation demonstrates a complete integration of mathematical modeling, physics simulation, and interactive graphics. The result is a responsive and visually intuitive Bézier rope simulation that satisfies all assignment requirements.
