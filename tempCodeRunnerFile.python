import tkinter as tk
import threading
import time


class TrafficLightApp:
   def __init__(self, root):
       self.root = root
       self.root.title("Traffic Light App")


       self.canvas = tk.Canvas(root, width=200, height=400, bg="black")
       self.canvas.pack()


       self.red_light = self.canvas.create_oval(50, 50, 150, 150, fill="grey")
       self.yellow_light = self.canvas.create_oval(50, 150, 150, 250, fill="grey")
       self.green_light = self.canvas.create_oval(50, 250, 150, 350, fill="grey")


       self.stop_event = threading.Event()
       self.current_thread = None


       self.btn_start = tk.Button(root, text="Start", command=self.start_normal)
       self.btn_start.pack(side=tk.TOP, padx=10, pady=10)


   def reset_lights(self):
       self.canvas.itemconfig(self.red_light, fill="grey")
       self.canvas.itemconfig(self.yellow_light, fill="grey")
       self.canvas.itemconfig(self.green_light, fill="grey")


   def stop_current_action(self):
       if self.current_thread and self.current_thread.is_alive():
           self.stop_event.set()
           self.current_thread.join()
       self.stop_event.clear()
       self.reset_lights()


   def start_normal(self):
       self.stop_current_action()
       self.current_thread = threading.Thread(target=self.normal_cycle)
       self.current_thread.start()


   def normal_cycle(self):
       while not self.stop_event.is_set():
           self.canvas.itemconfig(self.green_light, fill="green")
           time.sleep(2)
           if self.stop_event.is_set():
               break
           self.canvas.itemconfig(self.green_light, fill="grey")


  
           self.canvas.itemconfig(self.yellow_light, fill="yellow")
           time.sleep(1)
           if self.stop_event.is_set():
               break
           self.canvas.itemconfig(self.yellow_light, fill="grey")


           self.canvas.itemconfig(self.red_light, fill="red")
           time.sleep(5)
           if self.stop_event.is_set():
               break
           self.canvas.itemconfig(self.red_light, fill="grey")
       self.reset_lights()


if __name__ == "__main__":
   root = tk.Tk()
   app = TrafficLightApp(root)
   root.mainloop()
