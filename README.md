# PROYECTO-FINAL-GRUPO-A
# Juego de Nave "SPACEJAM"
Universiad: Universidad Privada Domingo Savio

![UPDS LOGO](https://github.com/matthewcf23/PROYECTO-FINAL-GRUPA-A/assets/151700413/aa8556e4-759a-4e92-9130-9bc9eed059e7)

Facultad: Ingenieria

Titulo del proyecto: Juegos de Naves "Space Jam"

Asignatura: Progamacion I

Nombres: 

- Matias Choque Flores

- Daniel Erick Cruz Miranda

- William Axl Padilla Valenzuela

Docente: Jaime Zambrana Chacon 

## Resumen 

Este es un juego básico creado con Pygame donde controlas a un jugador para esquivar enemigos.

Es un emocionante juego arcade desarrollado en Pygame, donde tu destreza y agilidad serán puestas a prueba. En este juego simple pero desafiante, controlas a un jugador con el objetivo de esquivar enemigos que caen desde la parte superior de la pantalla.

Mientras te desplazas hábilmente por la pantalla, también tendrás la oportunidad de recoger alimentos para aumentar tu puntuación.

## Abstract

This is a basic game created with Pygame where you control a player to avoid enemies.

It is an exciting arcade game developed in Pygame, where your skill and agility will be put to the test. In this simple but challenging game, you control a player with the goal of dodging enemies that fall from the top of the screen.

As you skillfully move around the screen, you will also have the opportunity to collect food to increase your score.

## DESARROLLO
### Marco Teorico:
Pygame es un conjunto de módulos de Python diseñado para escribir videojuegos. Proporciona funciones de bajo nivel para controlar dispositivos de entrada, ventana, sonido, etc.

Algunos conceptos clave que se aplican en este proyecto son:

- Sprites: imagen que se muestra en la pantalla y se puede mover.
- Game loop: bucle que se ejecuta continuamente para actualizar los sprites, manejar entrada del usuario, colisiones, etc.
- FPS: cuadros por segundo, controla cuan rápido se actualiza la pantalla.
- Eventos: acciones que ocurren mientras se ejecuta el juego, como presionar una tecla.
- Colisiones: cuando dos sprites tocan la misma área, permite detectar eventos como recolectar puntos o perder vida.

## Proyecto

El objetivo del proyecto era aplicar los conceptos aprendidos en clase para implementar un videojuego funcional utilizando Python y la librería Pygame.

Algunos de los conceptos implementados incluyen:

- Programación orientada a eventos
- Movimiento y colisiones
- Bucles de juego
- Sonido y música
- Interfaz gráfica sencilla

![GRUPO](https://github.com/matthewcf23/PROYECTO-FINAL-GRUPA-A/assets/151700413/4b02be69-66c9-496a-8281-bbb45d9105fc)

### Instalación de librerías
El proyecto utiliza las siguientes librerías con sus respectivas versiones:

- Python 3.8.2
- Pygame 2.1.2

Pygame se puede instalar mediante el gestor de paquetes pip:


        pip install pygame==2.1.2
### Diseño
La interfaz gráfica del juego es sencilla, mostrando en pantalla:

- El personaje jugador (cuadrado verde)
- Los enemigos como cuadrados azules
- Los puntos de energía como cuadrados rosas
- El fondo de pantalla con imagen de espacio
- Texto informativo del puntaje y vidas restantes

Los assets gráficos como sprites e imagenes están en formato PNG.

Para los sonidos se utilizan efectos en formato WAV Y MP3.

#### Funcionalidades Importantes

Las funcionalidades centrales que se implementaron son:

- Movimiento del jugador: uso de teclas WASD para transladar al personaje en la ventana

- Enemigos: caen desde la parte superior en lugares al azar para agregar dificultad

- Energía: ítems que aparecen en cualquier parte de la pantalla para sumar puntos

- Colisiones: se detecta cuando el jugador choca con enemigos o recoge energía invocando las funciones creadas

- Puntajes y vidas: se lleva un conteo que afecta el estado del juego y determina el game over


## Codigo fuente

        #Importar librerias
        import pygame
        import sys
        import random

        #Inciamos pygame y el mixer
        pygame.init()
        pygame.mixer.init() 

        #Crear las varibales que vamos a usar, la ventana, el titulo de la ventana
        ANCHO = (900)
        ALTO = (800)

        COLOR_JUGADOR = (118,238,198)
        COLOR_ENEMIGO = (28,134,238)
        COLOR_FOOD = (238,18,137)

        velocidad = 20

        x_inicio = 420
        y_inicio = 700

        puntaje = 0

        vidas = 3

        ventana = pygame.display.set_mode((ANCHO,ALTO))
        pygame.display.set_caption("Space Jam")

        #Crear los objetos que apareceran en la pantalla
        food_size = 30
        food_pos = [random.randint(0,ANCHO - food_size),random.randint(0,ALTO - food_size)]

        jugador_size = 30
        jugador_pos = [420,700]

        enemigo_size = 50
        enemigo_pos = [random.randint(0,ANCHO - enemigo_size),0]

        #Crear el bucle infinito y un reloj
        game_over = False
        clock = pygame.time.Clock()

        #Cargar las imagenes y los sonidos
        background_juego = pygame.image.load("background_juego2.png")
        background_go = pygame.image.load("background_go2.png")
        soundtrack = pygame.mixer.Sound("soundtrack.mp3")
        soundtrack.play()  
        food_sound = pygame.mixer.Sound("food.wav")
        crash = pygame.mixer.Sound("crash.wav")

        #Funciones de colision, restar vidas, y aumentar puntaje
        def detectar_colision_enemigo(jugador_pos,enemigo_pos):
        jx = jugador_pos[0]
        jy = jugador_pos[1]
        ex = enemigo_pos[0]
        ey = enemigo_pos[1]

    if (ex >= jx and ex <(jx + jugador_size)) or (jx >= ex and jx < (ex + enemigo_size)):
        if (ey >= jy and ey <(jy + jugador_size)) or (jy >= ey and jy < (ey + enemigo_size)):
            if detectar_colision_enemigo:
                crash.play()
                global vidas
                vidas -=1
            return True
    return False

        def detectar_colision_food(jugador_pos,food_pos):
        jx = jugador_pos[0]
        jy = jugador_pos[1]
        fx = food_pos[0]
        fy = food_pos[1]

    if (fx >= jx and fx <(jx + jugador_size)) or (jx >= fx and jx < (fx + food_size)):
        if (fy >= jy and fy <(jy + jugador_size)) or (jy >= fy and jy < (fy + food_size)):
            food_sound.play()
            global puntaje
            puntaje +=10
            return True
    return False

        #Bucle de juego
        while not game_over:
        for evento in pygame.event.get():
                if evento.type == pygame.QUIT:
                sys.exit()
        #Movimiento del jugador
        tecla_presionada = pygame.key.get_pressed() 

    x = jugador_pos[0]
    y = jugador_pos[1]

    if tecla_presionada[pygame.K_a]:
                x -= velocidad
    if tecla_presionada[pygame.K_d]:
                x += velocidad
    if tecla_presionada[pygame.K_w]:
                y -= velocidad
    if tecla_presionada[pygame.K_s]:
                y += velocidad
            
    jugador_pos[0] = x
    jugador_pos[1] = y

    #Insertar fondo, texto de puntaje y de vidas en la pantalla
    ventana.blit(background_juego, [0,0])
    
    texto_puntos = pygame.font.SysFont("Impact", 30)
    puntos = texto_puntos.render("Puntaje: " + str(puntaje), 1, (32,178,170))
    ventana.blit(puntos,(50,50))

    texto_vidas = pygame.font.SysFont("Impact", 30)
    text_vidas = texto_vidas.render("Vidas: " + str(vidas), 1, (32,178,170))
    ventana.blit(text_vidas,(ANCHO - 150,50))

    #Movimiento y posicion aleatoria de los enemigos
    if enemigo_pos[1] >= 0 and enemigo_pos[1] < ALTO:
        enemigo_pos[1] += 20
    else:
        enemigo_pos[0] = random.randint(0,ANCHO - enemigo_size)
        enemigo_pos[1] = 0

    #Llamar funciones de colision
    if detectar_colision_enemigo(jugador_pos,enemigo_pos):
        jugador_pos[0] = x_inicio
        jugador_pos[1] = y_inicio
        detectar_colision_enemigo(jugador_pos,enemigo_pos)
    
    if detectar_colision_food(jugador_pos,food_pos):
        food_pos[0] = random.randint(0,ANCHO - food_size)
        food_pos[1] = random.randint(0,ALTO - food_size)
        
    #Dibujar al enemigo, food, jugador; insertar puntos y vidas en la pantalla
    pygame.draw.rect(ventana,COLOR_ENEMIGO,(enemigo_pos[0],enemigo_pos[1],enemigo_size,enemigo_size))
    pygame.draw.rect(ventana,COLOR_FOOD,(food_pos[0],food_pos[1],food_size,food_size))
    pygame.draw.rect(ventana,COLOR_JUGADOR,(jugador_pos[0],jugador_pos[1],jugador_size,jugador_size))
    ventana.blit(puntos,(50,50))
    text_vidas = texto_vidas.render("Vidas: " + str(vidas), 1, (32,178,170))
    ventana.blit(text_vidas,(ANCHO - 150, 50))

    #Condicion para que la pantalla cambie cuando el jugador se quede sin vidas
    if vidas == 0:
        game_over = True

    #Condicion para cambiar la imagen y poner pantalla de game over
    if game_over:
        ventana.blit(background_go, [0,0])
        go_fuente = pygame.font.SysFont("Impact", 60)
        go_texto = go_fuente.render("GAME OVER", True, (255,255,255))
        ventana.blit(go_texto, (ANCHO//2 - go_texto.get_width()//2, ALTO//2 - go_texto.get_height()//2))
        pygame.display.update()
        game_over = False

    #Usar el reloj para controlar la velocidad de los enemigos
    clock.tick(30)

    #Actualizar pantalla
    pygame.display.update()
        pygame.quit()

## Conclusion
Este proyecto me permitió practicar conceptos importantes de programación como:

- Bucles infinitos y control de frames por segundo
- Manejo de eventos y entradas de teclado
- Posicionamiento y movimiento de sprites
- Detección de colisiones
- Actualización de puntajes y vidas
- Reproducción de sonidos y música

En general fue una gran experiencia para mejorar mnuestras habilidades en Pygame y aplicar varios conceptos importantes de programación de videojuegos.

## Descripción 

Desarrollamos este juego porque queríamos aplicar nuestras habilidades de programación en Python y Pygame para crear un juego divertido y desafiante.

Mi motivación fue poner a prueba mi conocimiento de detección de colisiones, movimiento aleatorio de enemigos, y creación de sistemas de puntos. Queríamos diseñar una buena experiencia de juego con controles simples e interacciones satisfactorias.

Al crear este juego, aprendimos:

- Técnicas de detección de colisión entre rectángulos
- Generación aleatoria de posiciones de los enemigos.
- Reproducción de sonidos con Pygame
- Control de flujo del juego con un bucle principal.

## Bibliografia

https://youtu.be/J473At9fuSk?si=1zXepp7SKMZ8nsxB
https://youtu.be/4ME4q7NXydI?si=S5tqUrHabPRZiRcw
https://youtu.be/yHg4sKkPEnc?si=epcWxfUSFj1mcgoN
https://youtu.be/rsMnvJolpVo?si=_tkZyRjPg9-lyuAC
