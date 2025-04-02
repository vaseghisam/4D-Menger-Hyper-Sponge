import numpy as np
import matplotlib.pyplot as plt

def menger_sponge_3d(level):
    """
    Build a 3D Menger sponge (20-cube variant) of recursion depth `level`.
    Returns a 3D NumPy boolean array (True = solid, False = removed).
    
    The rule: remove subcubes where >=2 coordinates == 1.
    """
    if level == 0:
        # Base case: a single voxel
        return np.ones((1, 1, 1), dtype=bool)
    
    prev = menger_sponge_3d(level - 1)
    n = prev.shape[0]
    new_n = n * 3
    
    sponge = np.zeros((new_n, new_n, new_n), dtype=bool)
    
    for i in range(3):
        for j in range(3):
            for k in range(3):
                # Count how many coordinates equal 1
                count_ones = (i == 1) + (j == 1) + (k == 1)
                # Skip subcubes if 2 or 3 of the coords are 1
                if count_ones >= 2:
                    continue
                sponge[i*n:(i+1)*n,
                       j*n:(j+1)*n,
                       k*n:(k+1)*n] = prev
    return sponge

# Example usage & visualization
if __name__ == "__main__":
    level = 3  # You can try 2, 3, or 4… but be careful with memory for large levels
    sponge_3d = menger_sponge_3d(level)
    fig = plt.figure(figsize=(8, 8))
    ax = fig.add_subplot(111, projection='3d')
    ax.voxels(sponge_3d, facecolors='red', edgecolor='k')
    ax.set_title(f"3D Menger Sponge (level={level}, 20-cube variant)")
    ax.axis('off')
    plt.show()
