# The camera file (war3map.w3c)
  
## File format

| Size | Description | 
| -----|-----|
| `int` | file version = 0 |
| `int` | number "NCAMS" of cameras |
| `camera[NCAMS]` | array of camera structures |

### Camera structure

| Size | Description | 
| -----|-----|
| `float` | Target X |
| `float` | Target Y |
| `float` | Z Offset |
| `float` | Rotation (angle in degree) |
| `float` | Angle Of Attack (AoA) (angle in degree) |
| `float` | Distance |
| `float` | Roll |
| `float` | Field of View (FoV) (angle in degree) |
| `float` | Far Clipping (FarZ) |
| `float` | unknown (usually set to 100) |
| `String` | Cinematic name |
