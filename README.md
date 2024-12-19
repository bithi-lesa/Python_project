# Predefined dye colors in RGB format (name, RGB tuple)
dye_colors = [

("Red", (255, 0, 0)),
("Green", (0, 255, 0)),
("Blue", (0, 0, 255)),
("Yellow", (255, 255, 0)),
("Cyan", (0, 255, 255)),
("Magenta", (255, 0, 255)),
("Black", (0, 0, 0)),
("White", (255, 255, 255)),
("Orange", (255, 165, 0)),
("Purple", (128, 0, 128)),
]
def rgb_to_hex(rgb):
"""Convert an RGB tuple to Hex format."""
return '#' + ''.join(f'{x:02X}' for x in rgb)
def hex_to_rgb(hex_color):
"""Convert a Hex color code to an RGB tuple."""
hex_color = hex_color.lstrip('#')
return tuple(int(hex_color[i:i + 2], 16) for i in (0, 2, 4))
def euclidean_distance(rgb1, rgb2):
"""Calculate the Euclidean distance between two RGB colors."""
return math.sqrt(sum((a - b) ** 2 for a, b in zip(rgb1, rgb2)))
def find_closest_color(input_color):
"""Find the closest match from the predefined dye colors."""
if isinstance(input_color, str) and input_color.startswith('#'):
# Input is in Hex format, convert to RGB
input_rgb = hex_to_rgb(input_color)
elif isinstance(input_color, tuple) and len(input_color) == 3:
# Input is already in RGB format
input_rgb = input_color
else:
raise ValueError("Invalid input format. Use RGB tuple or Hex
format.")
# Find the closest color by calculating the Euclidean distance
closest_color = None
min_distance = float('inf')
for color_name, dye_rgb in dye_colors:
distance = euclidean_distance(input_rgb, dye_rgb)
if distance < min_distance:
min_distance = distance
closest_color = (color_name, dye_rgb)
return closest_color
def main():
print("Welcome to the Color Matching Tool for Textile Dyeing!")

# Input color from user (either in RGB tuple or Hex format)
user_input = input("Enter the color (RGB tuple as (R, G, B) or Hex as
#RRGGBB): ").strip()
if user_input.startswith('(') and user_input.endswith(')'):
# RGB input
try:
rgb_values = tuple(map(int, user_input.strip('()').split(',')))
matched_color = find_closest_color(rgb_values)
except ValueError:
print("Invalid RGB input. Make sure it's in the format (R, G,
B).")
return
elif user_input.startswith('#'):
# Hex input
try:
matched_color = find_closest_color(user_input)
except ValueError:
print("Invalid Hex input. Make sure it's in the format #RRGGBB.")
return
else:
print("Invalid input format. Please use either RGB or Hex format.")
return
# Display the closest match
color_name, color_rgb = matched_color
color_hex = rgb_to_hex(color_rgb)
print(f"The closest dye color match is: {color_name} (RGB: {color_rgb},
Hex: {color_hex})")
if __name__ == "__main__":
main()# Python_project
