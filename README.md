# chocoding
Winter 23-24 Coding

## Winter 2023-24 Worklog
#### Week 5 (Jan 22 - Jan 28)

Triple star system (1.5 hours)

```
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
G = 6.67430e-11  # Gravitational constant
m = 1.989e30     # Mass of each star (in kg)
dt = 3600        # Time step in seconds
num_steps = 10000

# Initial conditions
r1 = np.array([0.5e12, 0, 0])  # Initial position of star 1 (in meters)
r2 = np.array([0, 0.5e12, 0])  # Initial position of star 2 (in meters)
r3 = np.array([0, 0, 0.5e12])  # Initial position of star 3 (in meters)
v1 = np.array([0.0, 1000.0, 0.0])    # Initial velocity of star 1 (in m/s)
v2 = np.array([0.0, 0.0, -1000.0])   # Initial velocity of star 2 (in m/s)
v3 = np.array([1000.0, 0.0, 0.0])    # Initial velocity of star 3 (in m/s)

# Arrays to store positions
positions1 = np.zeros((num_steps, 3))
positions2 = np.zeros((num_steps, 3))
positions3 = np.zeros((num_steps, 3))

# Euler integration method
for i in range(num_steps):
    # Calculate distances between stars
    r12 = np.linalg.norm(r2 - r1)
    r13 = np.linalg.norm(r3 - r1)
    r23 = np.linalg.norm(r3 - r2)
    
    # Calculate gravitational forces
    F12 = G * m**2 / r12**2
    F13 = G * m**2 / r13**2
    F23 = G * m**2 / r23**2
    
    # Calculate directions of forces
    direction12 = (r2 - r1) / r12
    direction13 = (r3 - r1) / r13
    direction23 = (r3 - r2) / r23
    
    # Calculate accelerations
    a1 = (F12 * direction12 + F13 * direction13) / m
    a2 = (-F12 * direction12 + F23 * direction23) / m
    a3 = (-F13 * direction13 - F23 * direction23) / m
    
    # Update velocities and positions
    v1 += (a1 * dt).astype(np.float64)
    v2 += (a2 * dt).astype(np.float64)
    v3 += (a3 * dt).astype(np.float64)

    r1 += (v1 * dt).astype(np.float64)
    r2 += (v2 * dt).astype(np.float64)
    r3 += (v3 * dt).astype(np.float64)
    
    # Store positions for plotting
    positions1[i] = r1
    positions2[i] = r2
    positions3[i] = r3

# Plotting
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

# Plotting trajectories
ax.plot(positions1[:, 0], positions1[:, 1], positions1[:, 2], label='Star 1')
ax.plot(positions2[:, 0], positions2[:, 1], positions2[:, 2], label='Star 2')
ax.plot(positions3[:, 0], positions3[:, 1], positions3[:, 2], label='Star 3')

# Plot initial positions
ax.scatter(r1[0], r1[1], r1[2], color='red', label='Initial Star 1')
ax.scatter(r2[0], r2[1], r2[2], color='blue', label='Initial Star 2')
ax.scatter(r3[0], r3[1], r3[2], color='green', label='Initial Star 3')

ax.set_xlabel('X-axis')
ax.set_ylabel('Y-axis')
ax.set_zlabel('Z-axis')
ax.legend()
plt.title('Three-Star System Motion')
plt.show()
```


<img width="619" alt="Screenshot 2024-01-29 at 20 26 38" src="https://github.com/yunacho1/chocoding/assets/150376499/9fc0f29f-7622-4cdb-b21f-55d4f89892e7">



Debugging vpython simulation (2 hours)

- Changed parameters such as velocity, mass, radius, and initial distance.
- Utilized Chat GPT, but did not help

```
from vpython import *

def main():
    # Simulate the motion of a binary system with one star more massive than the other

    # Define constants
    G = 6.67480e-11
    
    # Mass ratio
    mass_ratio = 0.11
    
    # Mass of the stars
    m_star1 = 1.9891e30  # Mass of the sun
    m_star2 = mass_ratio * m_star1  # less massive star
    
    # Radius of the stars (not to scale)
    r_star = 4e10
    
    # Initial distance between the stars
    initial_distance = 1e12
    
    # Create the objects
    star1 = sphere(pos=vector(-initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    star2 = sphere(pos=vector(initial_distance/2, 0, 0), radius=r_star, color=color.blue)
    
    # Set initial velocities
    star1.velocity = vector(0, -mass_ratio *7e3, 0)
    star2.velocity = vector(0, 7e3, 0)  # Adjusted velocity based on mass ratio
    
    # Define initial time
    t = 0
    
    # Define time interval
    dt = 1e4
    
    while t < 1e10:
        rate(300)
        
        # Update positions
        star1.pos = star1.pos + star1.velocity * dt
        star2.pos = star2.pos + star2.velocity * dt
        
        # Calculate gravitational forces
        r_vector = star1.pos - star2.pos
        F_grav = -(G * m_star1 * m_star2) / mag(r_vector)**2 * norm(r_vector)
        
        # Update velocities
        star1.velocity = star1.velocity + (F_grav / m_star1) * dt
        star2.velocity = star2.velocity - (F_grav / m_star2) * dt
        
        t += dt

main()
```


https://github.com/yunacho1/chocoding/assets/150376499/76839e5d-b481-4035-9b19-737d075ad0e9





#### Week 4 (Jan 15 - Jan 21)

Final Project Outline (1 hour)
- Find binary system information on journals
    - Contact binaries
- Enter the parameters on BM3
- Download simulation from BM3
- Code using the same parameters
- Comparison between BM3 and my Python simulation

Researched different code for binary system (0.5 hours)

[Github Reference](https://gist.github.com/andrelondono/e93422e36abe8787e414f735a7cb2581)

<img width="580" alt="Screenshot 2024-01-23 at 9 14 50" src="https://github.com/yunacho1/chocoding/assets/150376499/5d2391f3-6a10-49e9-ab6a-ae95c789ccde">

Did not work due to unidentified library, 'visual'. I had vpython but for some reason it could not find visual.

Coding and debugging (1 hour)

```
from vpython import *

def main():
    # Simulate the motion of a binary system with one star more massive than the other

    # Define constants
    G = 6.67480e-11
    
    # Mass ratio
    mass_ratio = 0.11
    
    # Mass of the stars
    m_star1 = 1.9891e30  # Mass of the sun
    m_star2 = mass_ratio * m_star1  # More massive star
    
    # Radius of the stars (not to scale)
    r_star = 5e10
    
    # Initial distance between the stars
    initial_distance = 1e11
    
    # Create the objects
    star1 = sphere(pos=vector(-initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    star2 = sphere(pos=vector(initial_distance/2, 0, 0), radius=r_star, color=color.blue)
    
    # Set initial velocities
    star1.velocity = vector(0, 1e3, 0)
    star2.velocity = vector(0, -mass_ratio * 1e3, 0)  # Adjusted velocity based on mass ratio
    
    # Define initial time
    t = 0
    
    # Define time interval
    dt = 1e4
    
    while t < 1e10:
        rate(300)
        
        # Update positions
        star1.pos = star1.pos + star1.velocity * dt
        star2.pos = star2.pos + star2.velocity * dt
        
        # Calculate gravitational forces
        r_vector = star1.pos - star2.pos
        F_grav = -(G * m_star1 * m_star2) / mag(r_vector)**2 * norm(r_vector)
        
        # Update velocities
        star1.velocity = star1.velocity + (F_grav / m_star1) * dt
        star2.velocity = star2.velocity - (F_grav / m_star2) * dt
        
        t += dt

main()

```

<img width="548" alt="Screenshot 2024-01-23 at 9 19 03" src="https://github.com/yunacho1/chocoding/assets/150376499/070acde4-1245-44b2-8a50-71bb235658e5">


My resulting binary star system with a star mass ratio of 0.11 ended up not working. I will look more into it in the following week.



Read the Binary Maker Manual (0.5 hours)

<img width="600" alt="Screenshot 2024-01-22 at 18 15 21" src="https://github.com/yunacho1/chocoding/assets/150376499/6db5ab2d-0f69-4cc8-8860-b02227a147f1">


Try contact binary star 
<img width="694" alt="Screenshot 2024-01-22 at 18 57 17" src="https://github.com/yunacho1/chocoding/assets/150376499/0f9a6ad1-1a5a-4f10-9e04-8433aa208cf3">



BM3: ASEriB 

<img width="599" alt="Screenshot 2024-01-22 at 18 10 07" src="https://github.com/yunacho1/chocoding/assets/150376499/2d5dc8c3-f0e9-4cba-9bdd-15abc87534b1">


https://github.com/yunacho1/chocoding/assets/150376499/608710b6-6c63-41e8-9df2-9eb011273970


Simulation on python with the same mass ratio


#### Week 3 (Jan 8 - Jan 14)
Plan:
- [ ] Match binary star system curve using BinaryMaker
- [x] Coding problems to practice coding
- [x] Research binary stars

Experimented with the BinaryMaker (0.5 hours)

Math behind binary star modeling (0.25 hours)

https://joss.tcnj.edu/wp-content/uploads/sites/176/2012/04/2012-Silano-Revised.pdf

Background research on binary stars (1 hour)

- Notes are on [binarystars.md](https://github.com/yunacho1/chocoding/blob/be246d5dfdab3ead4eab7eb11a4588af1334a4db/binarystars.md)

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

Simulation of binary star system with one star twice as massive as the other (1 hour)
- Attempted debugging with ChatGPT, but still has errors.

```
from vpython import *

def main():
    # Simulate the motion of a binary system with one star twice as massive as the other

    # Define constants
    G = 6.67480e-11
    
    # Mass of the stars
    m_star1 = 2 * 1.9891e30  # Twice the mass of the sun
    m_star2 = 1.9891e30  # Mass of the sun
    
    # Radius of the stars (not to scale)
    r_star = 2e10
    
    # Initial distance between the stars
    initial_distance = 1e11
    
    # Create the objects
    star1 = sphere(pos=vector(-initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    star2 = sphere(pos=vector(initial_distance/2, 0, 0), radius=r_star, color=color.yellow)
    
    # Set initial velocities
    star1.velocity = vector(0, 1e4, 0)  # Adjusted initial velocity
    star2.velocity = vector(0, -1e4, 0)  # Adjusted initial velocity
    
    # Define initial time
    t = 0
    
    # Define time interval
    dt = 1e4 
    
    while t < 1e10:
        rate(300)
        
        # Update positions
        star1.pos = star1.pos + star1.velocity * dt
        star2.pos = star2.pos + star2.velocity * dt
        
        # Calculate gravitational forces
        r_vector = star1.pos - star2.pos
        F_grav = -(G * m_star1 * m_star2) / mag(r_vector)**2 * norm(r_vector)
        
        # Update velocities
        star1.velocity = star1.velocity + (F_grav / m_star1) * dt
        star2.velocity = star2.velocity - (F_grav / m_star2) * dt
        
        t += dt

main()
```


https://github.com/yunacho1/chocoding/assets/150376499/31b1cc66-9b11-4dcb-ab15-021807559428


<img width="549" alt="Screenshot 2024-01-16 at 14 30 05" src="https://github.com/yunacho1/chocoding/assets/150376499/0a138233-f4b7-46bf-8a4a-c6ea2f4b10d0">

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
- Created a [field guide](https://github.com/yunacho1/chocoding/blob/9e66feb10031af39febc42b5b37fc2b51040f2b8/bm3fieldguide) for BinaryMaker (1.5 hour)
<img width="1440" alt="Screenshot 2023-12-12 at 6 46 41" src="https://github.com/yunacho1/yunacho1/assets/150376499/235bec51-bb46-481a-880e-978107dd8bb3">


Ideas:
- Simulate the solar system
- Explore machine learning in astronomy
- Simulate binary star systems using PyGame

<!---
yunacho1/yunacho1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
