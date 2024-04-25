# Lab4

En este laboratorio vamos a rear un robot cartesiano de 3 dimensiones, el robot será únicamente visual, en este caso vamos a usar la página web "URDF Visualizer" para verificar su diseño. Despues en el Plot Juggler vamos a graficar y analizar el funcionamiento del ultimo laboratorio.Demostraremos que el error final es 0 o muy cercano a 0, luego graficar la evolución de ATG y DTG.Correr su programa en bucle, al menos 4 veces, crear un ROSBAG y después plotear el experimentocompleto en PlotJuggler.

comenzamos con el robot visual de 3 dimenciones en URDF Visualizer,a continuacion se muestra el codigo o XML que describe la estructura y las propiedades de un robot simple de tipo cartesiano
```
<?xml version="1.0"?>
<robot name="simple_cartesian_robot">

  <!-- Material definitions -->
  <material name="mat1">
    <color rgba="0.5 0.5 0.5 1"/>
  </material>

  <!-- Base link -->
  <link name="base_link">
    <visual>
      <geometry>
        <box size="0.3 0.3 0.1"/>
      </geometry>
      <material name="mat1"/>
    </visual>
  </link>

  <!-- Link X -->
  <link name="link_x">
    <visual>
      <geometry>
        <cylinder radius="0.06" length="0.7"/>
      </geometry>
      <material name="mat1"/>
    </visual>
  </link>

  <!-- Joint for X movement -->
  <joint name="joint_x" type="prismatic">
    <origin xyz="0 0 1" rpy="0 0 0"/>
    <parent link="base_link"/>
    <child link="link_x"/>
    <axis xyz="1 0 0"/>
    <limit lower="0" upper="1" effort="1000" velocity="0.5"/>
  </joint>

  <!-- Link Y -->
  <link name="link_y">
    <visual>
      <geometry>
        <cylinder radius="0.06" length="0.7"/>
      </geometry>
      <material name="mat1"/>
    </visual>
  </link>

  <!-- Joint for Y movement -->
  <joint name="joint_y" type="prismatic">
    <origin xyz="1 0 0" rpy="0 0 0"/>
    <parent link="link_x"/>
    <child link="link_y"/>
    <axis xyz="0 1 0"/>
    <limit lower="0" upper="1" effort="1000" velocity="0.5"/>
  </joint>

  <!-- Link Z -->
  <link name="link_z">
    <visual>
      <geometry>
        <cylinder radius="0.06" length="0.7"/>
      </geometry>
      <material name="mat1"/>
    </visual>
  </link>

  <!-- Joint for Z movement -->
  <joint name="joint_z" type="prismatic">
    <origin xyz="0 1 0" rpy="0 0 0"/>
    <parent link="link_y"/>
    <child link="link_z"/>
    <axis xyz="0 0 1"/>
    <limit lower="-1" upper="0" effort="1000" velocity="0.5"/>
  </joint>

</robot>
```
