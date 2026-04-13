# particle-detector-simulation
# Simulation of a particle detector with a charged particle trajectory. Gaussian noise is added to mimic experimental uncertainty, and 
# linear regression is used to reconstruct the path. Demonstrates data analysis and scientific computing using Python.


import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# PARAMÈTRES
# -----------------------------
np.random.seed(42)

n_points = 50        # nombre de points mesurés
noise_level = 0.5    # bruit du détecteur

# -----------------------------
# TRAJECTOIRE RÉELLE
# -----------------------------
x_true = np.linspace(0, 10, n_points)
y_true = 2 * x_true + 1   # droite : y = 2x + 1

# -----------------------------
# MESURES AVEC BRUIT
# -----------------------------
noise = np.random.normal(0, noise_level, n_points)
y_measured = y_true + noise

# -----------------------------
# RECONSTRUCTION (fit linéaire)
# -----------------------------
coeffs = np.polyfit(x_true, y_measured, 1)
y_fit = np.polyval(coeffs, x_true)

# -----------------------------
# AFFICHAGE
# -----------------------------
plt.figure()

plt.scatter(x_true, y_measured, label="Mesures (bruitées)")
plt.plot(x_true, y_true, linestyle="--", label="Trajectoire réelle")
plt.plot(x_true, y_fit, label="Trajectoire reconstruite")

plt.xlabel("Position x")
plt.ylabel("Position y")
plt.title("Simulation d'un détecteur de particules")

plt.legend()
plt.grid()

plt.show()

# -----------------------------
# AFFICHAGE DES PARAMÈTRES
# -----------------------------
print("Trajectoire réelle : y = 2x + 1")
print(f"Trajectoire reconstruite : y = {coeffs[0]:.2f}x + {coeffs[1]:.2f}")
