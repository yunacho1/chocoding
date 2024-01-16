# chocoding
Winter 23-24 Coding

## Winter 2023-24 Worklog
#### Week 3 (Jan 8 - Jan 14)
Plan:
- [ ] Match binary star system curve using BinaryMaker
- [x] Coding problems to practice coding
- [x] Research binary stars

Programmed a simulation of binary star system using Python (1 hour)
```
dfdd
```

Coding practice: C++ (1.5 hours)


#### Week 2 + Winter Break (Dec 11 - Dec 15, - Jan 7)
Plan
- [x] Practice coding using Java
- [x] Study about ScikitLearn (2 hours)

Coding practice: 3 hours (Java: 1 hour)
Went on https://www.acmicpc.net/, a coding practice website to practice coding with Java and C++.

<img width="543" alt="Screenshot 2024-01-08 at 14 22 05" src="https://github.com/yunacho1/chocoding/assets/150376499/9712a463-655b-4eaa-89c5-8fea251ce1b0">

Scikit Learn Tutorial: 2 hours 
https://www.youtube.com/watch?v=0B5eIE_1vpU

Notes from Tutorial:
* Machine Learning library
* Part 1: Scikit-Learn
  * Version 0.23.0
  * Install Scikit Learn first
* Part 2: Preprocessing
* Part 3: Metrics
* Part 4: Meta Estimators
* Part 5: Human-Learn 


#### Week 1 (Dec 4 - Dec 10)
Work:
- Read and watched GitHub tutorials (0.5 hours)
- Created a list of coding ideas (1 hour)
  - [ChatGPT Reference Convo](https://chat.openai.com/share/ab351e6c-b8e8-44e3-9c11-a639c52c63b9)
- Coding: Simulation of the motion of the first four planets (1 hour)
  - Used Pygame and known constants to simulate the motion of Mercury, Venus, Earth, and Mars.
```
import pygame
import math

# Constants for the simulation (not to scale)
WIDTH, HEIGHT = 800, 600  # Screen dimensions
G = 6.674 * (10 ** -11)   # Gravitational constant
AU = 149.6 * (10 ** 9)    # 1 AU (Astronomical Unit) in meters

# Planet data (semi-major axis in AU, orbital period in Earth days)
planet_data = {
    'Mercury': {'semi_major_axis': 0.39, 'orbital_period': 88.0},
    'Venus': {'semi_major_axis': 0.72, 'orbital_period': 224.7},
    'Earth': {'semi_major_axis': 1.0, 'orbital_period': 365.2},
    'Mars': {'semi_major_axis': 1.52, 'orbital_period': 687.0}
}

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Solar System Simulation")

# Colors
WHITE = (255, 255, 255)
YELLOW = (255, 255, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Function to calculate position based on time
def calculate_position(semi_major_axis, orbital_period, time):
    angle = (2 * math.pi * time) / orbital_period
    x = semi_major_axis * AU * math.cos(angle)
    y = semi_major_axis * AU * math.sin(angle)
    return x, y

# Main simulation loop
clock = pygame.time.Clock()
time_passed = 0

running = True
while running:
    screen.fill(WHITE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Simulate and draw planets
    for planet_name, data in planet_data.items():
        semi_major_axis = data['semi_major_axis']
        orbital_period = data['orbital_period']
        x, y = calculate_position(semi_major_axis, orbital_period, time_passed)
        radius = 5  # Radius of the planet (not to scale)
        
        # Adjust positions to fit on the screen
        screen_x = int((x / (1.5 * AU)) * WIDTH) + WIDTH // 2
        screen_y = int((y / (1.5 * AU)) * HEIGHT) + HEIGHT // 2
        
        # Draw planets
        if planet_name == 'Mercury':
            pygame.draw.circle(screen, RED, (screen_x, screen_y), radius)
        elif planet_name == 'Venus':
            pygame.draw.circle(screen, GREEN, (screen_x, screen_y), radius)
        elif planet_name == 'Earth':
            pygame.draw.circle(screen, BLUE, (screen_x, screen_y), radius)
        elif planet_name == 'Mars':
            pygame.draw.circle(screen, YELLOW, (screen_x, screen_y), radius)

    pygame.display.flip()
    time_passed += 1  # Time increment for simulation (can be adjusted for speed)

    clock.tick(60)  # Limit to 60 frames per second

pygame.quit()
```
- Installed Java, Editor MD, BinaryMaker (0.5 hours)
- Studied the manual (1 hour)
- Explored the different functions and adjusted parameters (1 hour)
- Created a field guide for BinaryMaker (1.5 hour)
<img width="1440" alt="Screenshot 2023-12-12 at 6 46 41" src="https://github.com/yunacho1/yunacho1/assets/150376499/235bec51-bb46-481a-880e-978107dd8bb3">


Ideas:
- Simulate the solar system
- Explore machine learning in astronomy
- Simulate binary star systems using PyGame

<!---
yunacho1/yunacho1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
