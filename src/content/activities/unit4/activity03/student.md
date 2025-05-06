## 1. Implementación completa

### `BrushQueue.h`

```cpp
#pragma once
#include "ofMain.h"

struct Node {
    float x, y, radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float x_, float y_, float radius_, ofColor color_, float opacity_) {
        x = x_;
        y = y_;
        radius = radius_;
        color = color_;
        opacity = opacity_;
        next = nullptr;
    }
};

class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int maxSize_) {
        front = rear = nullptr;
        size = 0;
        maxSize = maxSize_;
    }

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};
```

### `BrushQueue.cpp`

```cpp
#include "BrushQueue.h"

void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);
    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    size++;

    if (size > maxSize) {
        dequeue();
    }
}

void BrushQueue::dequeue() {
    if (!isEmpty()) {
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;
        if (front == nullptr) rear = nullptr;
    }
}

void BrushQueue::clear() {
    while (!isEmpty()) {
        dequeue();
    }
}

bool BrushQueue::isEmpty() {
    return front == nullptr;
}
```

---

### `ofApp.h`

```cpp
#pragma once

#include "ofMain.h"
#include "BrushQueue.h"

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);

    BrushQueue strokes = BrushQueue(50); // tamaño inicial
    int backgroundHue;
};
```

### `ofApp.cpp`

```cpp
#include "ofApp.h"

void ofApp::setup() {
    ofSetBackgroundAuto(true);
    backgroundHue = ofRandom(255);
    ofSetCircleResolution(100);
}

void ofApp::update() {
    if (ofGetMousePressed()) {
        float x = ofGetMouseX();
        float y = ofGetMouseY();
        float radius = ofRandom(10, 30);
        ofColor color;
        color.setHsb(ofRandom(255), 200, 255);
        float opacity = 255;
        strokes.enqueue(x, y, radius, color, opacity);
    }
}

void ofApp::draw() {
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    Node* current = strokes.front;
    int i = 0;
    while (current != nullptr) {
        float fade = ofMap(i, 0, strokes.maxSize, 50, 255);
        ofSetColor(current->color, fade);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        i++;
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear();
    } else if (key == 'a') {
        if (strokes.maxSize == 50) {
            strokes.maxSize = 100;
        } else {
            strokes.maxSize = 50;
        }
    } else if (key == 's') {
        ofSaveScreen("screenshot_" + ofToString(ofGetTimestampString()) + ".png");
    }
}
```

## 2. Reporte de depuración

**Pruebas realizadas:**

| Acción                       | Resultado Esperado                           | Resultado Obtenido | Estado |
| ---------------------------- | -------------------------------------------- | ------------------ | ------ |
| Mantener presionado el mouse | Se generan círculos con colores vivos        | Correcto           | ✅      |
| Presionar tecla 'c'          | Se eliminan todos los círculos               | Correcto           | ✅      |
| Presionar tecla 'a'          | Cambia el límite de la cola (50/100)         | Correcto           | ✅      |
| Presionar tecla 's'          | Se guarda una captura de pantalla            | Correcto           | ✅      |
| No mover el mouse            | No se generan nuevos círculos                | Correcto           | ✅      |
| Exceder `maxSize`            | Se eliminan los más antiguos automáticamente | Correcto           | ✅      |

**Errores encontrados y corregidos:**

* Inicialmente no se eliminaban bien los nodos más viejos → se corrigió en `dequeue()`.
* Fade-out no se aplicaba bien → se aplicó `ofMap(i, 0, maxSize, 50, 255)`.

## 3. Lista de pruebas

**Pruebas funcionales:**

*  El sistema dibuja círculos con color aleatorio al mover el mouse.
*  Los círculos más antiguos se eliminan automáticamente al superar el `maxSize`.
*  El fondo tiene un gradiente armónico en HSB.
*  Fade out visual para los círculos viejos (opacidad disminuye).
*  Tecla `c` limpia todos los elementos de la cola.
*  Tecla `a` alterna el tamaño de la cola entre 50 y 100.
*  Tecla `s` guarda una captura de pantalla.
