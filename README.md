# ros_commons

Este pacote foi desenvolvido como parte de uma disciplina de robótica, com o objetivo de reunir recursos compartilhados entre diferentes simulações do projeto ROSbot 3. Ele agrupa utilidades de configuração, macros URDF e lançadores que apoiam o desenvolvimento e a validação de novos comportamentos para o robô.

## Conteúdo
- `config/steering.rqt`: layout salvo do painel RQT para teleoperação diferencial do robô.
- `launch/rqt.launch` e `launch/rqt_steering.launch`: lançadores prontos para abrir a interface RQT com os plugins necessários para monitorar tópicos e publicar comandos de velocidade.
- `urdf/domain.xacro`: macros genéricas reutilizadas em múltiplas descrições do robô.
- `urdf/gazebo.xacro`: extensões específicas para simulação no Gazebo, incluindo sensores e controladores.

## Adições relevantes
- Macro `skid_steer_controller` em `urdf/gazebo.xacro`, permitindo configurar facilmente um controlador diferencial com dois pares de rodas, incluindo publicação opcional de odometria e TFs.
- Ajustes nas macros de sensores (`depth_camera` e `lidar_2d`) para oferecer remapeamentos padrão de tópicos e parâmetros de atualização compatíveis com os testes em aula.

## Como utilizar
1. Adicione `ros_commons` como dependência do seu pacote na simulação.
2. Inclua as macros necessárias dentro dos seus arquivos `.xacro`, por exemplo:
   ```xml
   <xacro:include filename="$(find ros_commons)/urdf/gazebo.xacro"/>
   <xacro:skid_steer_controller
     name="skid_steer_controller"
     publish_odom="true"
     left_joint_0="joint_wheel_front_left"
     right_joint_0="joint_wheel_front_right"
     left_joint_1="joint_wheel_rear_left"
     right_joint_1="joint_wheel_rear_right"
     wheel_separation_0="${wheel_separation}"
     wheel_diameter_0="${wheel_diameter}"
     wheel_separation_1="${wheel_separation}"
     wheel_diameter_1="${wheel_diameter}"
   />
   ```
3. Utilize os lançadores RQT para inspeção rápida dos tópicos de interesse durante os experimentos.

