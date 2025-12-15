Interactive Bézier Rope Simulation

This project focuses on building an interactive cubic Bézier curve that behaves like a soft, flexible rope. The curve reacts smoothly to mouse movement, creating a realistic sense of elasticity. Along with the curve, tangent directions are displayed to help visualize how the curve changes direction at different points. All calculations and motion logic are implemented manually without relying on any built-in Bézier or physics tools.

The curve is constructed using four control points. The first and last points remain fixed to act as anchors, while the two middle control points are allowed to move freely. For any value of t between 0 and 1, the position of the curve is computed using the cubic Bézier formula: B(t) = (1−t)³P₀ + 3(1−t)²tP₁ + 3(1−t)t²P₂ + t³P₃. The final curve is drawn by evaluating this equation at regular intervals and connecting the resulting points.

To better understand the curve’s shape, tangent vectors are calculated using the derivative of the Bézier equation. These vectors represent the direction of the curve at specific points. After normalization, the tangents are drawn as short line segments along the curve, making changes in curvature easy to observe.

The motion of the movable control points is controlled using a spring-damping physics model. Each point moves toward a target position influenced by mouse input, but instead of jumping directly to that position, it follows smooth, physics-based motion. The acceleration is calculated using a combination of spring force and damping, and positions are updated using Euler integration. This approach produces natural movement with slight delay, similar to how a real rope behaves.

Mouse movement continuously updates the target positions of the inner control points. Since the control points respond through the spring system rather than directly, the curve feels flexible and responsive instead of stiff or mechanical.

During each animation frame, the physics calculations are updated, the Bézier curve is recalculated, and the scene is redrawn. The curve, tangent lines, and control points are rendered using the HTML Canvas API. The animation loop runs with requestAnimationFrame, ensuring smooth performance close to 60 frames per second.

Overall, this implementation combines mathematical curve modeling, basic physics simulation, and real-time rendering into a single interactive visualization. The result is a clean and efficient Bézier rope simulation that clearly demonstrates curve behavior and dynamic motion without relying on external libraries.
