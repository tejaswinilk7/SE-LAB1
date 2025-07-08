import matplotlib.pyplot as plt

# Step 1: Input 3 data points from the user
print("Enter 3 (x, y) data points:")

points = []
for i in range(1, 4):
    x = float(input(f"Enter x{i}: "))
    y = float(input(f"Enter y{i}: "))
    points.append((x, y))

# Unpack the points
(x1, y1), (x2, y2), (x3, y3) = points

# Step 2: Form equations manually
# a*x^2 + b*x + c = y
# So:
# a1 = x1^2, b1 = x1, c1 = 1
# a2 = x2^2, ...
A1 = [x1**2, x1, 1]
A2 = [x2**2, x2, 1]
A3 = [x3**2, x3, 1]

# Right-hand side values
Y1, Y2, Y3 = y1, y2, y3

# Step 3: Solve using substitution method (manual)

# Form equation A = A2 - A1
A = [A2[i] - A1[i] for i in range(3)]
Y_A = Y2 - Y1

# Form equation B = A3 - A2
B = [A3[i] - A2[i] for i in range(3)]
Y_B = Y3 - Y2

# Subtract A from B to eliminate c and get a
# A:  aA + bB + cC = Y_A
# B:  aD + bE + cF = Y_B
# Subtract B - A → solve for a
a = (Y_B * A[1] - Y_A * B[1]) / (B[0] * A[1] - A[0] * B[1])

# Solve for b using equation A
b = (Y_A - A[0] * a) / A[1]

# Solve for c using first equation
c = Y1 - (a * x1**2 + b * x1)

# Step 4: Print coefficients
print(f"\nQuadratic equation: y = {a:.4f}x² + {b:.4f}x + {c:.4f}")

# Step 5: Plot the result
def quadratic(x):
    return a * x**2 + b * x + c

# Generate x values and corresponding y values
x_values = [x for x in range(int(min(x1, x2, x3)) - 2, int(max(x1, x2, x3)) + 3)]
y_values = [quadratic(x) for x in x_values]

# Plot the quadratic curve
plt.plot(x_values, y_values, label="Quadratic Curve", color='blue')

# Plot original points
data_x = [x1, x2, x3]
data_y = [y1, y2, y3]
plt.scatter(data_x, data_y, color='red', label="Given Points")

# Labeling
plt.title("Quadratic Curve from Keyboard Input")
plt.xlabel("x")
plt.ylabel("y")
plt.grid(True)
plt.legend()
plt.show()
