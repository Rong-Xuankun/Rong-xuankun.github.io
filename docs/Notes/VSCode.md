# VSCode



命令面板：⇧⌘P

添加行注释：⌘/ 

添加块注释：⌥⇧A

代码提示：⌘I（`I` refers to `IntelliSense`）

双击选中一个词，三击选中一行

⌥左右 和 ⌘上下左右；⇧光标区域选中；⇧上下左右 和 ⇧⌥左右 和 ⌘⇧上下左右

⌥⌫、⌘⌫；fn⌫

⌘C和⌘X可以对一行生效

⌥点击多处添加多个光标



**修改快捷键：**

⌘K+⌘S 打开快捷键设置





## settings.json

**全局/用户设置和工作区设置**

打开设置，可以看到有两栏基本一样的设置。先说工作区设置：工作区设置修改之后只对当前的文件夹（项目）起作用；而用户设置指的是无论你用`VS Code`打开哪个文件夹（项目），`VS Code`都会用这些设置；相当于你修改了用户设置，这个设置全局有效，改一次用户设置相当于改了好多个工作区的设置，所以我下面会将用户设置称作全局设置。

注：工作区设置和用户/全局设置同时存在时，工作区的设置起作用/优先级高/覆盖。

**使用工作区设置的优点**

确保你以后在写别的代码（开了别的文件夹/接了新的项目）的时候不会受某次设置的影响