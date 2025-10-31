
# Evidencias de la unidad 8

![moving-psychedelic-pattern-neon-light-streaks-free-video](https://github.com/user-attachments/assets/0baa4037-8919-445c-bec3-946317bbb96e)
![textura-marmol-fondo-liquido-abstracto-diseno-acuarela-ondas-tinta_629210-310](https://github.com/user-attachments/assets/b238f37c-6d04-459b-babb-b4fcb3e60ba9)
![colorido-caleidoscopio-flores-muestra-sobre-fondo-negro_860805-1614](https://github.com/user-attachments/assets/ace87616-ddba-4f90-ab01-09d0b600349f)

Mi inspiracion para esta unidad es los visuales psicodelicos, tipo caleidoscopio, basandome en el arte geometrico, abstracto y la distorcion visual. Para esto usare una cancion y los visuales reaccionan a ella, la idea es que con el celular se controlen las luces y con el microbit aparezcan girasoles.
VERSION 1:
cpp
```
#include "ofApp.h"

// --------------------------------------------------------------------------------------
// SETUP: Se ejecuta una sola vez al inicio
// --------------------------------------------------------------------------------------
void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
    ofDisableArbTex();

    // Carga del Shader
    if (ofIsGLProgrammableRenderer()) {
        shader.load("shadersGL3/shader");
    }
    else {
        shader.load("shadersGL2/shader");
    }

    // Carga de la Imagen
    if (img.load("img.jpg")) {
        img.getTexture().setTextureWrap(GL_REPEAT, GL_REPEAT);
    }
    else {
        ofLogError("ofApp::setup") << "No se pudo cargar la imagen 'img.jpg'.";
        img.allocate(512, 512, OF_IMAGE_COLOR);
        img.setColor(255);
        img.update();
        img.getTexture().setTextureWrap(GL_REPEAT, GL_REPEAT);
    }

    plane.set(ofGetWidth(), ofGetHeight(), 2, 2);
    plane.mapTexCoords(0, 0, 1, 1);

    numSegments = 6.0;
    angleOffset = 0.0;

    // --- INTEGRACIÓN DE AUDIO ---
    // Carga de la Canción: ¡Debe estar en bin/data!
    if (song.load("sunflower.mp3")) {
        song.setVolume(0.75);
        song.setLoop(true);
        song.play();
    }
    else {
        ofLogError("ofApp::setup") << "Error al cargar 'sunflower.mp3'. Asegúrate de que está en bin/data.";
    }

    // Inicialización para el Análisis de Frecuencias (FFT)
    N_BINS = 512; // Define el número de bandas para el espectro
    fftSmoothed.resize(N_BINS, 0.0f); // Inicializa el vector de suavizado
    beatValue = 0.0f;
    voiceValue = 0.0f;
}

// --------------------------------------------------------------------------------------
// UPDATE: Se ejecuta en cada frame
// --------------------------------------------------------------------------------------
void ofApp::update() {
    ofSoundUpdate(); // ¡Fundamental! Actualiza el motor de audio

    angleOffset = ofGetElapsedTimef() * 0.1;

    // --- ANÁLISIS DE AUDIO ---
    float* val = ofSoundGetSpectrum(N_BINS); // Obtiene el espectro de frecuencias

    // 1. Suavizado del Espectro
    for (int i = 0; i < N_BINS; i++) {
        fftSmoothed[i] *= 0.9f; // Decaimiento (suaviza la caída)
        if (val[i] > fftSmoothed[i]) {
            fftSmoothed[i] = val[i]; // Si el valor actual es mayor, lo tomamos
        }
    }

    // --- 2. EXTRACCIÓN DE CARACTERÍSTICAS ---

    // a) Frecuencias Bajas (Ondas)
    float lowFreqEnergy = 0.0f;
    int lowBins = 64; // Bandas 0 a 63 (bajos)
    for (int i = 0; i < lowBins; i++) {
        lowFreqEnergy += fftSmoothed[i];
    }
    lowFreqEnergy /= lowBins;
    lowFreqEnergy *= 10.0f; // Multiplicador para hacerlo visible
    lowFreqEnergy = ofClamp(lowFreqEnergy, 0.0f, 1.0f);

    // Mapear bajos al rango de onda (0.0 a 0.15)
    beatValue = ofMap(lowFreqEnergy, 0.0f, 1.0f, 0.0f, 0.15f);


    // b) Frecuencias Medias/Altas (Voces)
    float midHighEnergy = 0.0f;
    int midHighStart = 64; // Inicio del rango vocal
    int midHighEnd = 256; // Fin del rango vocal
    int midHighCount = midHighEnd - midHighStart;

    for (int i = midHighStart; i < midHighEnd; i++) {
        midHighEnergy += fftSmoothed[i];
    }
    midHighEnergy /= midHighCount;
    midHighEnergy *= 10.0f; // Multiplicador
    midHighEnergy = ofClamp(midHighEnergy, 0.0f, 1.0f);

    // Mapear el valor vocal. Lo usamos directamente de 0 a 1 para interpolación de color.
    voiceValue = midHighEnergy;
}

// --------------------------------------------------------------------------------------
// DRAW: Se ejecuta en cada frame para dibujar
// --------------------------------------------------------------------------------------
void ofApp::draw() {

    img.getTexture().bind();
    shader.begin();

    // Uniforms para el shader
    shader.setUniform1f("time", ofGetElapsedTimef());
    shader.setUniform1f("numSegments", numSegments);
    shader.setUniform1f("angleOffset", angleOffset);
    shader.setUniform2f("resolution", ofGetWidth(), ofGetHeight());

    // --- Uniforms de Audio ---
    shader.setUniform1f("audioIntensity", beatValue); // Control de Ondas (Ritmo)
    shader.setUniform1f("voiceValue", voiceValue);   // Control de Color (Voces)

    // Dibujo del Plano
    ofPushMatrix();
    ofTranslate(ofGetWidth() / 2, ofGetHeight() / 2);
    plane.draw();
    ofPopMatrix();

    shader.end();
    img.getTexture().unbind();

    // Texto de Información (Actualizado)
    ofSetColor(255);
    string info = "FPS: " + ofToString(ofGetFrameRate(), 2) + "\n";
    info += "Segments (UP/DOWN): " + ofToString(numSegments, 0) + "\n";
    info += "Audio Intensity (ONDAS): " + ofToString(beatValue, 4) + "\n";
    info += "Voice Value (COLOR): " + ofToString(voiceValue, 4);
    ofDrawBitmapString(info, 20, 20);
}

// --------------------------------------------------------------------------------------
// Funciones de Eventos (Sin cambios)
// --------------------------------------------------------------------------------------
void ofApp::keyPressed(int key) {

    if (key == OF_KEY_UP) {
        numSegments++;
    }
    if (key == OF_KEY_DOWN) {
        numSegments = max(3.0f, numSegments - 1.0f);
    }
}

void ofApp::keyReleased(int key) {}
void ofApp::mouseMoved(int x, int y) {}
void ofApp::mouseDragged(int x, int y, int button) {}
void ofApp::mousePressed(int x, int y, int button) {}
void ofApp::mouseReleased(int x, int y, int button) {}

void ofApp::windowResized(int w, int h) {

    plane.set(w, h, 2, 2);
    plane.mapTexCoords(0, 0, 1, 1);
}

void ofApp::gotMessage(ofMessage msg) {}
void ofApp::dragEvent(ofDragInfo dragInfo) {}
```
h
```
#pragma once

#include "ofMain.h"
#include <vector> // Necesario para std::vector<float>

class ofApp : public ofBaseApp {
public:

    void setup();
    void update();
    void draw();

    void keyPressed(int key);
    void keyReleased(int key);
    void mouseMoved(int x, int y);
    void mouseDragged(int x, int y, int button);
    void mousePressed(int x, int y, int button);
    void mouseReleased(int x, int y, int button);
    void windowResized(int w, int h);
    void dragEvent(ofDragInfo dragInfo);
    void gotMessage(ofMessage msg);

    ofShader shader;
    ofPlanePrimitive plane;
    ofImage img;

    // Parámetros de control para el caleidoscopio
    float numSegments;
    float angleOffset;

    // --- INTEGRACIÓN DE AUDIO ---
    ofSoundPlayer song;
    float beatValue;    // Control de ondas (ritmo)
    float voiceValue;   // Control de color (voces)
    std::vector<float> fftSmoothed;
    int N_BINS;
    // ----------------------------
};
```
vert
```
#version 150

// Atributos de entrada del vértice
in vec4 position;
in vec2 texcoord;

// Atributos que pasamos al fragment shader
out vec2 vTexCoord;

// Uniforms (valores globales de la aplicación)
uniform mat4 modelViewProjectionMatrix;
// Aunque no se usa aquí, se declara si se pasa por el pipeline (es mejor ponerlo en el frag)
// uniform float time; 

void main() {
    // Transforma la posición del vértice al espacio de clip
    gl_Position = modelViewProjectionMatrix * position;

    // Pasa las coordenadas de textura al fragment shader
    vTexCoord = texcoord;
}
```
frag
```
#version 150

// Atributos de entrada del vertex shader
in vec2 vTexCoord;

// Uniforms (valores globales de la aplicación)
uniform sampler2D tex0;
uniform vec2 resolution;
uniform float audioIntensity; // Control de Ondas (ritmo)
uniform float voiceValue;     // ¡NUEVO! Control de Color (voces)
uniform float numSegments;
uniform float angleOffset;
uniform float time;

out vec4 fragColor;

const float PI = 3.14159265359;

// Función para cambiar de color de forma suave (HSL a RGB simplificado)
// Basado en iq's hsv->rgb, usamos el tono (h) que cambia con el tiempo.
vec3 hsv2rgb(float h, float s, float v) {
    vec4 t = vec4(1.0, 2.0 / 3.0, 1.0 / 3.0, 3.0);
    vec3 p = abs(fract(vec3(h) + t.xyz) * 6.0 - t.w);
    return v * mix(vec3(t.x), clamp(p - t.x, 0.0, 1.0), s);
}

void main() {

    // 1. Coordenadas centradas y corregidas por aspecto
    vec2 pos = vTexCoord - 0.5;
    pos.x *= resolution.x / resolution.y;

    // --- INTERACCIÓN CON EL AUDIO: DISTORSIÓN DE ONDA ---
    float waveIntensity = audioIntensity;
    float zoomFactor = 1.8; // Valor fijo para el zoom

    vec2 distortedPos = pos;
    // Distorsión de Onda (reacciona a audioIntensity)
    distortedPos.x += cos(pos.y * 15.0 + time * 3.0) * waveIntensity;
    distortedPos.y += sin(pos.x * 12.0 + time * 2.5) * waveIntensity;

    pos = distortedPos;

    // --- 2. APLICAR CALEIDOSCOPIO Y ZOOM ---
    vec2 centerOffset = vec2(0.0, 0.0);
    pos -= centerOffset;
    pos *= zoomFactor;

    // 3. Conversión a coordenadas polares para el caleidoscopio
    float r = length(pos);
    float a = atan(pos.y, pos.x);

    // 4. Lógica del Caleidoscopio (Reflejo)
    float segmentAngle = 2.0 * PI / numSegments;
    a = mod(a + angleOffset, 2.0 * PI);
    a = abs(a - segmentAngle * floor(a / segmentAngle + 0.5));
    a = abs(a - segmentAngle * 0.5);

    // 5. Conversión de vuelta a coordenadas cartesianas
    vec2 finalTexCoord = vec2(r * cos(a), r * sin(a));

    // 6. Mapear las coordenadas finales de nuevo al rango 0-1
    finalTexCoord = finalTexCoord + 0.5;

    // 7. Muestrear la textura con las coordenadas manipuladas
    vec4 textureColor = texture(tex0, finalTexCoord);

    // --- 8. CAMBIO DE COLOR POR VOZ ---

    // a) Tono que cambia lentamente con el tiempo
    float hue = mod(time * 0.1, 1.0);
    vec3 colorShift = hsv2rgb(hue, 1.0, 1.0);
    
    // b) Interpolar entre el color de la textura y el color de cambio.
    // voiceValue actúa como el factor de mezcla (0.0 = solo textura, 1.0 = colorShift puro).
    vec3 finalRGB = mix(textureColor.rgb, colorShift, voiceValue);

    fragColor = vec4(finalRGB, textureColor.a);
}
```
# PROCESOS:



https://github.com/user-attachments/assets/d1ef83c0-7698-4090-a090-421fc87579a6




https://github.com/user-attachments/assets/b9fc9edb-24b9-45ea-8d84-c4deea4544d6



https://github.com/user-attachments/assets/cda8ca87-d3a3-48de-b2e8-c4d68cde2d84

# AUTOV
| Ítem                | Descripción                                                 | Cumplimiento             | Valor (%) | Justificación                                                                                                                                                                                                      |
| ------------------- | ----------------------------------------------------------- | ------------------------ | --------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1                   | Actividad 1 (concepto, bitácora, evidencias, **diagrama**)  |  Parcialmente cumplida |        12 | Entregué concepto, bitácora y evidencias, **pero no** realicé el diagrama.                                                                                                                                         |
| 2                   | Actividad 2 (proyecto 100% funcional y presentado en clase) | Cumplida completamente |        12 | Proyecto completo, funcional y presentado en clase según la exigencia.                                                                                                                                             |
| 3                   | Autoevaluación                                              | Cumplida completamente |        12 | Autoevaluación realizada con reflexión y honestidad.                                                                                                                                                               |
| **Resultado final** | **Nivel según rúbrica**                                     | **Nota = 4**             |           | Realicé la actividad 1 casi por completo (falta el diagrama), la actividad 2 está completa y funcional y presenté en clase; además hice la autoevaluación. Según la rúbrica, esto corresponde a una **nota de 4**. |

