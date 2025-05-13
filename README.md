
<img align="right" width="26%" src="./misc/logo.png">

Entropy
===

A C++ library for generating noise data

---

## Installation

### CMake

```cmake
FetchContent_Declare(
  entropy
  GIT_REPOSITORY https://github.com/bresilla/entropy.git
  GIT_TAG        main
)
FetchContent_MakeAvailable(entropy)


target_link_libraries(<lib/bin> PRIVATE entropy::entropy)
```

---

## Usage

```cpp
#include <entropy/noisegen.hpp>

// Create and configure FastNoise object
NoiseGen noise;
noise.SetNoiseType(NoiseGen::NoiseType_OpenSimplex2);

// Gather noise data
std::vector<float> noiseData(128 * 128);
int index = 0;

for (int y = 0; y < 128; y++)
{
    for (int x = 0; x < 128; x++)
    {
        noiseData[index++] = noise.GetNoise((float)x, (float)y);
    }
}
```

---

Basically a copy modification of [FastNoiseLite](https://github.com/Auburn/FastNoiseLite) by [Auburn](https://github.com/Auburn).
