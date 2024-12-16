+++
date = '2023-04-06T15:00:53+01:00'
draft = false
title = 'VRPSolverEasy: a Python library for the exact solution of a rich vehicle routing problem'
+++
# 

## Project Overview

VRPSolverEasy is an advanced optimization library designed to solve Vehicle Routing Problems (VRP) and its variants using sophisticated Branch and Price algorithms. The project provides a comprehensive solution for researchers and practitioners in logistics, transportation, and optimization.

## Repository
🔗 **GitHub**: [https://github.com/inria-UFF/VRPSolverEasy/](https://github.com/inria-UFF/VRPSolverEasy/)

## Article
📄 **Publication**: [VRPSolverEasy: A Python Library for the Exact Solution of a Rich Vehicle Routing Problem](https://pubsonline.informs.org/doi/abs/10.1287/ijoc.2023.0103)

## Technical Architecture

### Core Technologies
- **Languages**: C++, Python
- **Field**: Integer Linear Programming
- **Optimization Techniques**: Branch and Cut and Price Algorithm

### Key Components
1. **C++ Optimization Core**
   - High-performance solving engine
   - Implements BCP model
   - Efficient memory management
   - Low-level optimization techniques
   - Design pattern 

2. **Python Wrapper**
   - Pythonic interface for model creation
   - Easy-to-use modeling abstractions
   - Dynamic problem specification
   - Seamless integration with scientific computing ecosystem

## Mathematical Foundation: Branch and Cut and Price Algorithm

### Theoretical Background

Branch and Cut and Price is an advanced solution method for solving complex combinatorial optimization problems, particularly effective for Vehicle Routing Problems.

#### Algorithmic Stages

1. **Column Generation**
   - Dynamically generate potential solution routes
   - Solve relaxed linear programming problem
   - Identify promising route candidates

2. **Branching**
   - Recursively divide solution space
   - Explore different route configurations
   - Prune infeasible or suboptimal branches
   - Example : Strong branching
   

3. **Cutting**
    - Apply valid inequalities to tighten problem formulation
    - Strengthen linear programming relaxation
    - Improve solution quality
   -  Example : Rank 1-Cut , Rounded capacity cuts


## Multiplatform Deployment

### Supported Platforms

- macOS 
- Windows
- Linux

### Deployment Strategies
- Shared libraries
- Python package distribution
- Compatible with major OS architectures

## Development Highlights

### Technical Challenges
- Cross-platform compilation
- Efficient wrapper implementation
- Performance optimization
- Numerical stability

### Wrapper Development
- **C++ to Python Bridge**
  - ctypes integration
  - Type conversion mechanisms
  - Error handling Json serialization

### Optimization Model Workflow
1. Problem definition
2. Model construction
3. Constraint specification
4. Solution generation
5. Result analysis

## Python Modeling Interface

### Example Usage Snippet
```python
import VRPSolverEasy as vrpse
import math

def compute_euclidean_distance(x_i, x_j, y_i, y_j):
    """compute the euclidean distance between 2 points from graph"""
    return round(math.sqrt((x_i - x_j)**2 +
                           (y_i - y_j)**2), 3)

# Data
cost_per_distance = 10
begin_time = 0
end_time = 5000
nb_point = 7

# Map with names and coordinates
coordinates = {"Wisconsin, USA": (44.50, -89.50),  # depot
               "West Virginia, USA": (39.000000, -80.500000),
               "Vermont, USA": (44.000000, -72.699997),
               "Texas, the USA": (31.000000, -100.000000),
               "South Dakota, the US": (44.500000, -100.000000),
               "Rhode Island, the US": (41.742325, -71.742332),
               "Oregon, the US": (44.000000, -120.500000)
               }

# Demands of points
demands = [0, 500, 300, 600, 658, 741, 436]

# Initialisation
model = vrpse.Model()

# Add vehicle type
model.add_vehicle_type(
    id=1,
    start_point_id=0,
    end_point_id=0,
    name="VEH1",
    capacity=1100,
    max_number=6,
    var_cost_dist=cost_per_distance,
    tw_end=5000)

# Add depot
model.add_depot(id=0, name="D1", tw_begin=0, tw_end=5000)

coordinates_keys = list(coordinates.keys())
# Add customers
for i in range(1, nb_point):
    model.add_customer(
        id=i,
        name=coordinates_keys[i],
        demand=demands[i],
        tw_begin=begin_time,
        tw_end=end_time)

# Add links
coordinates_values = list(coordinates.values())
for i in range(0, 7):
    for j in range(i + 1, 7):
        dist = compute_euclidean_distance(coordinates_values[i][0],
                                          coordinates_values[j][0],
                                          coordinates_values[i][1],
                                          coordinates_values[j][1])
        model.add_link(
            start_point_id=i,
            end_point_id=j,
            distance=dist,
            time=dist)

# solve model
model.solve()
model.export()

if model.solution.is_defined():
    print(model.solution)
```

## Performance Characteristics

- **Scalability**: Handles large-scale routing problems
- **Flexibility**: Supports multiple VRP variants
- **Precision**: Advanced mathematical modeling
- **Speed**: Optimized solving strategies

## Research and Collaboration

### Institutional Support
- Inria (French National Institute for Research in Computer Science and Automation)
- UFF (Fluminense Federal University)

## Future Roadmap

- Enhanced algorithm implementations
- More VRP variant support
- Integration of machine learning branching strategies
- Performance benchmarking

## Contribution and Community

- Open-source development
- Academic collaboration
- Continuous algorithm improvement

### How to Contribute
1. Fork repository
2. Create feature branch
3. Implement improvements
4. Submit pull request


