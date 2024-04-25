# Lab4

En este laboratorio vamos a rear un robot cartesiano de 3 dimensiones, el robot será únicamente visual, en este caso vamos a usar la página web "URDF Visualizer" para verificar su diseño. Despues en el Plot Juggler vamos a graficar y analizar el funcionamiento del ultimo laboratorio.Demostraremos que el error final es 0 o muy cercano a 0, luego graficar la evolución de ATG y DTG.Correr su programa en bucle, al menos 4 veces, crear un ROSBAG y después plotear el experimentocompleto en PlotJuggler.

comenzamos con el robot visual de 3 dimenciones en URDF Visualizer,a continuacion se muestra el codigo o XML que describe la estructura y las propiedades de un robot simple de tipo cartesiano: 
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
Definimos los componentes físicos del robot, en este caso tenemos 3 enlaces : "base_link", "link_x", "link_y" y "link_z". Cada enlace tiene una parte visual que define su apariencia gráfica utilizando formas geométricas como cajas o cilindros.

En las juntas <joint>: Define las articulaciones del robot que conectan los enlaces entre sí, los tres joints son de tipo prismatic, lo que significa que se mueven en línea recta, estas juntas son:
* joint_x: Une "base_link" y "link_x" permitiendo el movimiento en el eje X.
* joint_y: Une "link_x" y "link_y" permitiendo el movimiento en el eje Y.
* joint_z: Une "link_y" y "link_z" permitiendo el movimiento en el eje Z.

Propiedades de las juntas <limit>: Se definen límites para cada articulación que restringen su movimiento. Estos límites están definidos por valores como la posición máxima y mínima, el esfuerzo máximo y la velocidad máxima.

Orígenes y ejes de las juntas <origin> y <axis>: Estos elementos definen la ubicación y orientación inicial de las juntas con respecto a los enlaces que conectan, así como la dirección en la que se permite el movimiento.

Para obtener la tabla de Denavit-Hartenberg (DH) en este caso como todas las juntas son de tipo prismatico, la tabla DH será relativamente simple, la cual queda como:
![image](https://github.com/andre261220/Lab4/assets/157633777/6a2aed1a-b4dc-446b-90b3-969e1795a65f)

y la visualizacion del robot seria la siguiente:
![image](https://github.com/andre261220/Lab4/assets/157633777/80e2b9ec-8bc7-4a4e-b59d-bd72e9637daa)
en este caso se pueden ajustar los eslabones que solo tenemos 3 y todos prismaticos.
