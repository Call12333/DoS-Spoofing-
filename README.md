Informe Técnico: Inundación CDP (CDP Flooding)
Este proyecto documenta la simulación de un ataque de inundación sobre el protocolo CDP (Cisco Discovery Protocol). El objetivo es analizar cómo reacciona el plano de control de un dispositivo de red Cisco ante un volumen masivo de anuncios de vecinos falsos.

🛡️ Descripción del Ataque
El CDP Flooding consiste en enviar miles de paquetes CDP malformados o con identidades falsas hacia un switch o router.

Impacto: Aunque no siempre satura la tabla de vecinos (dependiendo de la validación del IOS), el ataque obliga a la CPU del dispositivo a procesar cada paquete, verificar el checksum y analizar los campos TLV, lo que puede elevar el consumo de recursos y ocultar dispositivos legítimos.

💻 Análisis del Script (Python + Scapy)
El script genera paquetes encapsulados específicamente para ser reconocidos por hardware Cisco:

Estructura del Paquete Inyectado:
Capa 2 (Ethernet): Utiliza la dirección MAC de destino multicast de Cisco: 01:00:0c:cc:cc:cc.

Encapsulación LLC/SNAP: Necesaria para que el tráfico sea interpretado como CDP.

Campos TLV (Type-Length-Value): El script genera dinámicamente:

Device ID: Nombres de dispositivos aleatorios.

Port ID: Puertos falsos (ej. FastEthernet 0/1, Gigabit 0/5).

Platform: Modelos de switches simulados.

Version: Cadenas de texto que emulan el software IOS.

<img width="517" height="438" alt="image" src="https://github.com/user-attachments/assets/1d47e0f1-3cd3-416f-b555-c10254412202" />

<img width="439" height="348" alt="image" src="https://github.com/user-attachments/assets/befb0386-33b0-4cc8-91d3-48f59d3e31c5" />
