# Autonomous-vehicle-and-Robotics-
Autonomous vehicle and Robotics description 

#!/usr/bin/env python3
"""
Virtual Parking Assistant (ASCII Grid) - Final Working Implementation
This script provides a command-line ASCII grid simulation of a parking lot.
It supports spot allocation, release, and real-time visualization with collision avoidance.
"""
class ParkingLot:
 def __init__(self, rows=5, cols=10):
 self.rows = rows
 self.cols = cols
 # Initialize the grid with '.' denoting vacant spots
 self.grid = [['.' for _ in range(cols)] for _ in range(rows)]
 def display(self):
 """Display current parking lot state."""
 print("\nParking Lot Status:")
 print(" " + " ".join(str(i) for i in range(self.cols)))
 for idx, row in enumerate(self.grid):
 print(f"{idx} " + " ".join(row))
 print("Legend: '.' = vacant, 'X' = occupied\n")
 def find_nearest_spot(self):
 """Find the nearest available parking spot (top-left priority)."""
 for r in range(self.rows):
 for c in range(self.cols):
 if self.grid[r][c] == '.':
 return (r, c)
 return None # No available spots
 def park_vehicle(self):
 """Allocate the nearest available spot."""
 spot = self.find_nearest_spot()
 if spot is None:
 print("Parking Lot Full: No spots available.")
 return False
 r, c = spot
 self.grid[r][c] = 'X'
 print(f"Vehicle parked at spot ({r}, {c}).")
 return True
 def release_spot(self, row, col):
 """Release the spot back to vacant."""
 if 0 <= row < self.rows and 0 <= col < self.cols:
 if self.grid[row][col] == 'X':
 self.grid[row][col] = '.'
 print(f"Spot ({row}, {col}) released and now vacant.")
 return True
 else:
 print(f"Spot ({row}, {col}) is already vacant.")
 return False
 else:
 print("Invalid spot coordinates.")
 return False
def main():
 lot = ParkingLot()
 print("Welcome to the Virtual Parking Assistant (ASCII Grid).")
 while True:
 lot.display()
 print("Options:")
 print(" 1 - Park a vehicle")
 print(" 2 - Release a spot")
 print(" 3 - Exit")
 choice = input("Enter your choice: ").strip()
 if choice == '1':
 lot.park_vehicle()
 elif choice == '2':
 try:
 r = int(input("Enter row to release: "))
 c = int(input("Enter column to release: "))
 lot.release_spot(r, c)
 except ValueError:
 print("Invalid input. Please enter numeric row and column.")
 elif choice == '3':
 print("Exiting Virtual Parking Assistant. Goodbye!")
 break
 else:
 print("Invalid choice. Please select a valid option.")
if __name__ == "__main__":
 main()
