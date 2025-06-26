# TheMixer
Mixer is a universal development environment, decompiler, compiler, runtime, and language translation system. Its purpose is to bridge the gap between all programming languages, architectures, and platforms by offering a unified pipeline for writing, analyzing, and launching software — regardless of origin or format.

**MixerIDE**

MixerIDE is an experimental, modular IDE designed to :

  - Accept source code from *any* language (C, Python, GML, Assembly, etc.)
  - Decompile unknown binaries or executables
  - Translate all inputs down to a universal low-level representation (e.g., Assembly)
  - Recompile into desired output formats (`.mix`, `.exe`, `.dmg`, etc.)
  - Analyze and correct code using optional AI-based debugging
  - Launch programs natively across different architectures and systems

# # Key Concept

# 1 : Language-agnostic development

Mix doesn't prioritize a specific language. Projects may contain multiple language blocks simultaneously, for example:
```lang
StartOf[Python]:
	def greet():
		print("Python is here !")

StartOF[C++]:
	void greet() {
		std::cout << "C++ is here too !";
  }
```
# 2 : OverLapTable System GUI system

In the case where the used languages will both take a same GUI window, the OverLapTable command will serve as an organization between each StartOf from any language that will modify the GUI. It will do so thanks to layered GUI-
For example, if the wanted languages are GML and Godot, which are repeated among the global Mix program, and will act over the GUI :

```lang
  StartOf[GML]:
    button_main = button_create(100, 100, 150, 40, "Start Game");
    button_set_color(button_main, c_green);

  StartOf[Godot]:
    var background = ColorRect.new()
    background.color = Color(0.1, 0.1, 0.3)
    background.rect_min_size = Vector2(640, 480)
    add_child(background)

  StartOf[GML]:
    draw_text(50, 30, "Score: " + string(global.score));

  StartOf[Godot]:
    var label = Label.new()
    label.text = "Welcome to Mix Demo"
    label.rect_position = Vector2(200, 20)
    add_child(label)
```

From that program, we can set the which StartOf[lang] goes on top of which, like this :
```lang
OverLapTable: [
  from GML : StartOf(1), LayerSetting = Opacity(90) + AlwaysFront;
  from Godot : StartOf(1), LayerSetting = AlwaysBack;
  from GML : StartOf(2), LayerSetting = Opacity(100);
  from Godot : StartOf(2), LayerSetting = Opacity(25);
]
```
The order of the layers in that block will put the upper-positioned layers more on the front, and the lower-positioned layers more on the back. The LayerSetting = AlwaysBack/Front will override the previously mentionned rule. If several AlwaysFront/Back are mentionned in the same block, you will be greeted with a crash. 

The OverLapTable can be used with either () or [], depending on wether you want the layering position to change over the program or not (works just like on Python).
Keep in mind that 3D and 2D layering are two different things- 2D layers will always be on top of 3D layers, and they follow the same rules, but on a different "Layer group".

# 3 : "Big Bang" method

This "Big Bang" method consists in taking a file from any source, and process them with the following steps : 
  - Decompile down to Assembly (compatible with file's original programming language ofc)
  - Analyze (by running)
  - Recompiling into an executable of a selected architecture, language, and/or device
(The file will get from small, high-layer programs to a CHUNKY file in Assembly, which is why it is called "Big Bang" method

# 4 : Executable deconstruction

Mix can accept compiled programs (or even game binaries, we'll see), then :
  - Detect the language or binary structure
  - Emulate/sandbox-run for analysis
  - Decompile + extract logic
  - Recompile into a modifiable .mix file, or native executale

# 5 : AI-Assisted Recovery (maybe)

While it's easier to go Upper → Lower programming layers (e.g. Python to C), going Lower → Upper (e.g., Assembly to C++, or bytecode to JavaScript) often requires AI assistance.

****Note: This project is in its early R&D phase.****

**Planned dependencies:**

Python (main framework)

LLVM / Clang (compilation backend)

Custom Assembly handling modules

AI module (optional; e.g., local LLM, or prompt-based engine)

UI system (Tkinter, Qt, or SDL depending on performance needs
