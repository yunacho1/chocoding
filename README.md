# chocoding
Winter 23-24 Coding

## Winter 2023-24 Worklog
#### Week 3 (Jan 8 - Jan 14)
Plan:
- [ ] Match binary star system curve using BinaryMaker
- [x] Coding problems to practice coding
- [x] Research binary stars

Programmed a simulation of binary star system of equal mass using Python (1 hour)
```
from vpython import *

def main():
    # Simulate the motion of a binary system with two stars of equal mass

    # Define constants
    G = 6.67480e-11
    
    # Mass of the stars
    m_star = 1.9891e30
    
    # Radius of the stars (not to scale)
    r_star = 2e10
    
    # Initial distance between the stars
    initial_distance = 1e11
    
    # Create the objects
    star1 = sphere(pos=vector(-initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    star2 = sphere(pos=vector(initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    
    # Set initial velocities
    star1.velocity = vector(0, 3e4, 0)
    star2.velocity = vector(0, -3e4, 0)
    
    # Define initial time
    t = 0
    
    # Define time interval
    dt = 3600
    
    while t < 1e10:
        rate(3000)
        
        # Update positions
        star1.pos = star1.pos + star1.velocity * dt
        star2.pos = star2.pos + star2.velocity * dt
        
        # Calculate gravitational forces
        r_vector = star1.pos - star2.pos
        F_grav = -(G * m_star**2) / mag(r_vector)**2 * norm(r_vector)
        
        # Update velocities
        star1.velocity = star1.velocity + (F_grav / m_star) * dt
        star2.velocity = star2.velocity - (F_grav / m_star) * dt
        
        t += dt

main()
```

Results


https://github.com/yunacho1/chocoding/assets/150376499/84465e63-7e2e-4a6c-814e-16131d765ce2


<img width="639" alt="Screenshot 2024-01-16 at 11 03 45" src="https://github.com/yunacho1/chocoding/assets/150376499/7b637fe8-8713-45ea-b2fa-27685c551d51">
<img width="633" alt="Screenshot 2024-01-16 at 11 04 01" src="https://github.com/yunacho1/chocoding/assets/150376499/06e64358-5c22-446d-9273-29ae6d1a1564">

Coding practice: C++ (1.5 hours)
- Learned about binary search
- <img width="408" alt="Screenshot 2024-01-16 at 11 11 53" src="https://github.com/yunacho1/chocoding/assets/150376499/628c6d2f-1120-4f46-a491-8071150bc91c">

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
