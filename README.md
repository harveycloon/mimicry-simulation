# mimicry-simulation
import pygame
import random

# Initialize pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("🦎 Mimicry Simulation 🦋")

# Load background images (mimicry environment)
environments = [
    pygame.image.load("forest.png"), 
    pygame.image.load("desert.png"), 
    pygame.image.load("ocean.png")
]

# Load mimicry creature images
creatures = {
    "forest": pygame.image.load("chameleon.png"),
    "desert": pygame.image.load("lizard.png"),
    "ocean": pygame.image.load("octopus.png")
}

# Resize images
environments = [pygame.transform.scale(img, (WIDTH, HEIGHT)) for img in environments]
for key in creatures:
    creatures[key] = pygame.transform.scale(creatures[key], (100, 100))

# Mimicry class
class MimicryCreature:
    def __init__(self):
        self.x = WIDTH // 2 - 50
        self.y = HEIGHT // 2 - 50
        self.environment = "forest"
        self.image = creatures[self.environment]
    
    def change_environment(self):
        self.environment = random.choice(["forest", "desert", "ocean"])
        self.image = creatures[self.environment]
    
    def draw(self, screen):
        screen.blit(self.image, (self.x, self.y))

# Create mimicry creature
mimic = MimicryCreature()

running = True
clock = pygame.time.Clock()

while running:
    screen.blit(environments[["forest", "desert", "ocean"].index(mimic.environment)], (0, 0))
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN and event.key == pygame.K_SPACE:
            mimic.change_environment()
    
    mimic.draw(screen)
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
