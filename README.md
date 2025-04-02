# 4D-Menger-Hyper-Sponge
4D Menger Hyper-Sponge

This Jupyter Notebook contains two code snippets, one that creates 3D Menger sponge and one that deals with the 4D Menger hyper-sponge.
The Notebook is supplementary material to an article, published on Medium:
https://medium.com/the-quantastic-journal/how-to-design-a-4d-hyper-fractal-the-magic-menger-hyper-sponge-9e9b3f5184a9


# 3D Menger Sponge

Build a 3D Menger sponge (20-cube variant) of recursion depth `level`.

Returns a 3D NumPy boolean array (True = solid, False = removed).

The rule: remove subcubes where >=2 coordinates == 1.



# 4D Menger Hyper-Sponge

Build a 4D Menger sponge via recursive integer subdivision.

At each level, the hypercube is subdivided into 3^4 sub-hypercubes.

For 4D, we remove those sub-hypercubes in which three or more of the indices equal 1.

(i.e. we keep a sub-hypercube if the count of ones in (i,j,k,l) is <= 2.)

We can choose both the fractal iteration level and the method used to generate the 4D Menger sponge slices; there are two options:

i) The integer method uses the exact, recursive subdivision of the unit hypercube. This builds a 4D boolean array of size $(3^{level})^4$. Slicing that array along the fourth axis gives exact, perfectly symmetric cross‑sections. The function `hyper_menger_sponge_4d_integer`(level) recursively subdivides the hypercube by applying an exact integer indexing.

ii) The rational method, where for each 3D slice, the program computes the membership on‑the‑fly by applying exact rational arithmetic with Python's Fraction type. One can choose the 3D resolution $N$ to set how many sample points per axis, and the depth, defined as the number of ternary digits checked, set equal to the iteration level. Because all arithmetic is exact, this minimizes floating‑point artifacts. Noteworthy that here we sample the continuous fractal rather than building its full tensor. Each point $(x,y,z,w)$ is treated as an exact Fraction. The function `in_hyper_menger_4d_rational()` checks the ternary digits exactly (up to the given level) such that the points get classified correctly without floating‑point error. The function `generate_3d_slice_rational()` builds a 3D slice for a given w value by sampling a grid of $N×N×N$ points.

Practically, one can select the method by setting the method parameter to either 'integer' or 'rational'. For the integer method, the fractal's resolution is automatically $(3^{level})$ in each axis; for the rational method, the user must provide a resolution $N$. The function `animate_sponge()` chooses which method to use. For the integer method, it extracts slices from the precomputed 4D tensor; for the rational method, it computes a sequence of 3D slices for w values, uniformly sampled in $[0,1]$.
