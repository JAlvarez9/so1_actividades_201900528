# Activdad 4

## Script utilizado

```text
#!/bin/bash
fecha=`date +"%d-%m-%Y %H:%M:%S"`
echo "Hola, esta es la actividad 4. Fecha $fecha" | systemd-cat -p info
```

## Creacion de un archivo de servicio

Se debe crear en el `system` (carpeta) y se debe guardar con el nombre de  `miservicio.service`
```text
[Unit]
Description=SO1_Actividad4_201900528
[Service]
ExecStart=/usr/local/bin/script.sh
[Install]
WantedBy=multi-user.target
```

## Comandos para utilizacion

```text
sudo systemctl status miservicio
sudo systemctl start miservicio
sudo systemctl status miservicio
```

Si todo salio bien deberiamos obtener este resultado
```text
mar 20 15:24:23 fabian systemd[1]: Inicio SO1_Actividad4_201900528.
mar 20 15:24:23 fabian cat[21301]: Hola, esta es la actividad 4. Fecha 20-03-2023 15:24:23
```

