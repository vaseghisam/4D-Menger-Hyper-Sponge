# 4D Menger Hyper-Sponge

Two Python scripts construct a 3D Menger sponge and animate 3D slices of a 4D Menger hyper-sponge. They accompany [How to Design a 4D Hyper-Fractal: The Magic Menger Hyper-Sponge](https://medium.com/the-quantastic-journal/how-to-design-a-4d-hyper-fractal-the-magic-menger-hyper-sponge-9e9b3f5184a9).

## Files

| File | Purpose |
| --- | --- |
| `Menger_3D.py` | Construct a 3D Boolean voxel array and display a Matplotlib figure |
| `Menger_4D.py` | Construct or sample 4D geometry, animate its 3D slices and save an MP4 |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT licence |

The supplied programs are Python scripts. No notebook file is included.

## Setup

Use Python 3. From the repository folder, install the dependencies:

```bash
python -m pip install -r requirements.txt
```

The 4D script imports IPython for its optional notebook display expression, so IPython is included in the dependencies even when the script runs from a terminal.

MP4 export also needs a system installation of FFmpeg on `PATH`. Check it with:

```bash
ffmpeg -version
```

## Run

Display the 3D sponge:

```bash
python Menger_3D.py
```

This opens a Matplotlib plot window. Close the window to finish the program.

Generate the 4D slice animation:

```bash
python Menger_4D.py
```

The animation is saved as `menger_4d.mp4` in the current working directory. Running the script again replaces that file.

## Parameters

In `Menger_3D.py`, change `level` in the example at the end of the file. Its default is 3.

In `Menger_4D.py`, the example at the end of the file defines:

| Parameter | Default | Meaning |
| --- | --- | --- |
| `chosen_level` | `2` | Number of subdivision levels or ternary digits checked |
| `chosen_method` | `'rational'` | Choose `'integer'` or `'rational'` |
| `resolution` | `20` | Samples per spatial axis for the rational method |
| `num_frames` | `10` | Number of requested fourth-coordinate slices |

## Construction methods

The 3D rule removes a subcube when at least two subdivision indices equal 1. It keeps 20 of the 27 subcubes at each level.

The 4D rule removes a sub-hypercube when at least three subdivision indices equal 1. It keeps 72 of the 81 sub-hypercubes at each level.

The integer method recursively builds a Boolean array with shape `(3**level, 3**level, 3**level, 3**level)` and extracts slices along its fourth axis. Memory use grows with the full four-dimensional array. The `resolution` setting does not affect this method.

The rational method samples a spatial grid and checks ternary digits with Python's `Fraction` arithmetic, without constructing the full 4D array. Each fourth-coordinate sample is first converted from a float with `limit_denominator(3**level)`, so different requested frames can use the same resulting rational coordinate.

## Licence

See [LICENSE](LICENSE) for the MIT licence.
