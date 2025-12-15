# Scissor Lift Visualizer

A web application to visualize the kinematics and geometry of a multi-stage scissor lift mechanism.

https://betanumeric.github.io/scissor_lift_visualizer/

## Controls

* **Arm Length**: Sets the physical length of the scissor arms in millimeters.

* **Stage Count**: Sets the number of scissor levels (1-10).

* **Interactive Preview**: Drag the platform, base slider, or actuator mount point to move the lift manually.

* **Play/Pause**: Toggles an animation that simulates a linear actuator moving at a constant speed.

* **Speed**: Adjusts the animation speed.

* **Actuator Level**: Selects which scissor stage the actuator is attached to.


## Maths

The visualizer uses trigonometry and vector geometry to solve the lift kinematics.

### 1. Lift Height ($H$)

The total height of the lift is determined by the Pythagorean theorem applied to a single scissor arm.

$$
H_{total} = N \times \sqrt{L^2 - W^2}
$$

* $H_{total}$: Total vertical height of the platform.

* $N$: Number of scissor stages.

* $L$: Length of a single scissor arm.

* $W$: Horizontal width of the base (distance between the fixed pivot and the sliding pivot).

### 2. Actuator Length ($L_{act}$)

The linear actuator connects the fixed base pivot (Origin) to a specific mounting point on one of the scissor arms. We calculate this length using vector interpolation.

Let the mounting position $u$ be a value from $0$ (bottom of the arm) to $1$ (top of the arm), and $k$ be the stage index where the actuator is attached.

The coordinates of the target mounting point $(x, y)$ are derived as:

$$
x = (1 - u) \cdot W
$$

$$
y = h_{stage} \cdot (k - 1 + u)
$$

Where $h_{stage} = \sqrt{L^2 - W^2}$.

The total length of the actuator is the magnitude of this vector:

$$
L_{act} = \sqrt{x^2 + y^2}
$$

### 3. Inverse Kinematics (Animation)

To simulate the actuator driving the lift, we solve the equation above for $W$ given a specific $L_{act}$. This requires solving a quadratic equation where $W^2$ is the unknown, allowing us to derive the specific base width required for any given actuator extension.

## Tech Stack

* **React**: UI state management and component structure.

* **HTML5 Canvas**: Rendering of the mechanical linkage and graphs.

* **Tailwind CSS**: Styling and layout.

* **Lucide React**: Icons.

* **Babel (Standalone)**: Compiles JSX in the browser.

