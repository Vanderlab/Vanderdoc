---
layout: post
title: midi controller tower #midi-controller-tower
date: 2017-03-03
permalink: projets/midi-controller-tower.html
---

## Tour de controle midi

# midi-controller-tower
Prototype : midi controller tower

Introduction
=====

Les DJ et musiciens manipulant l'électronique se tiennent souvent debout penchés sur leurs machines dans des positions peu ergonomiques. Pourquoi ne pas créer un contrôleur midi qui leur permette de se tenir droit pendant qu'ils jouent ?


Matériel
=====

* 12 Boutons-poussoirs Digitast type 1RT fugitif
* 4 Buzzers piezo à fils
* 4 Résistances 1MΩ
* 2 Joysticks 2 axes Parallax
* 1 Carte Arduino Mega 2560


Code
=====
```
/*
  midi controller tower made with an Arduino Mega connected to 18 sensors : 12 buttons, 4 Piezo and 2 Joysticks
  this code sends midi signals via the USB port in "serial format".
  You need to install Hairless-midiserial software on Mac or PC to translate that "serial" midi signal to your DAW (Digital Audio Workstation)
  http://projectgus.github.io/hairless-midiserial/
  For Windows users, you will also need to install Loopmidi
  http://www.tobias-erichsen.de/software/loopmidi.html
 */

// variables

byte NoteON = 144;         // NoteOn command         ( cf. protocole midi) http://computermusicresource.com/MIDI.Commands.html
byte ControlChange = 176;  // Control Change command ( cf. protocole midi) http://computermusicresource.com/MIDI.Commands.html

int ButtonPin[] ={10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21};  // Buttons Pin numbers (for the Arduino Mega)
byte NbButtons = 12;                                                // Number of Buttons
int ButtonState[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,0 };           // variable for reading the pushButton status
int PreviousButtonState[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };  // Variable to reccord last button state
int FirstPitchButton = 36;                                          // Lowest pitch of all the notes that can be played by the Buttons  36 => C2
int MajorKeyButton[] = {0, 2, 4, 5, 7, 9, 11, 12, 14, 16, 17, 19};  // Number of semitones for each note of a major Key

int PiezoPin[] = {A0, A1, A2, A3};                                  // Piezo Sensors Pin numbers
int NbPiezo = 4;                                                    // Number of Piezo sensors
int FirstPitchPiezo = 103;                                          // Pitch of the lowest note played by the Piezos 103 => G8
int MajorKeyPiezo[] = {0, 2, 4, 5, 7, 9, 11, 12, 14, 16};           // Number of semitones for each note of a major Key
int ThresholdPiezo = 10;                                            // Anything over the threshold means we've hit a Piezo
int DelayPiezo = 150;                                               // Delay minimum between two knock on a piezo

int Joystick[] = {A4, A5, A6, A7};                                  // Joysticks Pin numbers (using Arduino Mega)
int NbJoystick = 2;                                                 // Number of Joysticks
int JoystickPin = 0;                                                // Variable to record the Joystick current value
int JoystickValue[] = {0, 0, 0, 0};                                 // Joystick value mapped between 0 and 127 to be compatible with midi protocol
int PreviousJoystickValue[] = {0, 0, 0, 0};                         // Variable to record the Joystick last value


// functions

//  This function send a MIDI message via the serial port to the Hairless-midiserial software
void MIDImessage(byte NoteOrCmd, byte Pitch, byte velocity)
    {
    Serial.write(NoteOrCmd);
    Serial.write(Pitch);
    Serial.write(velocity);
    }


// the setup function runs once when you press reset or power the board
void setup() {

  Serial.begin(9600);                                              // 9600 bps rate if you communicate  via USB port (serial)

// initialize digital pin i as an input for the Buttons.
  for (int i=0; i<NbButtons; i++) {
  pinMode(ButtonPin[i], INPUT);
  digitalWrite(ButtonPin[i], HIGH);}                               // PullUP resistance activated        

} //end void setup()


void loop() {  

// Buttons sensors part

  for (int i=0; i<NbButtons; i++){
    // Read the state of the pushButton value:
    ButtonState[i] = digitalRead(ButtonPin[i]);
    int PitchButton = FirstPitchButton+MajorKeyButton[i];         // Pitch of the note to play
    // Check if the pushButton is pressed. if it is, the ButtonState is HIGH:
    if(PreviousButtonState[i] != ButtonState[i]){
      if (ButtonState[i] == HIGH) {
        PreviousButtonState[i] = ButtonState[i];                 // Backup the value of the button
        // Play note from FirstPitchButton+MajorKeyButton[i]
        MIDImessage(NoteON,PitchButton, 75);                     // Send the corresponding midi message to the serial port
        }
        else {
          PreviousButtonState[i] = ButtonState[i];
          // Stop the note (note off)
           MIDImessage(NoteON,PitchButton, 0);                   // Send the corresponding midi message to the serial port
            }
   } else {
    };
 }; // End of Buttons sensors part


// Piezo sensors part

  for (int i=0; i<NbPiezo; i++) {
    int PitchPiezo = FirstPitchPiezo+MajorKeyPiezo[i];
    int PiezoVal = analogRead(PiezoPin[i]);
    if (PiezoVal>ThresholdPiezo){            
      MIDImessage(NoteON, PitchPiezo, 80);                       // Play the midi note
      delay(DelayPiezo);
      MIDImessage(NoteON, PitchPiezo, 0);                        // Turn off the midi note
      }      
  }; // End of Piezo sensors part


// Joysticks sensors part

for (int i=0; i<NbJoystick*2; i++){
  JoystickPin = analogRead(Joystick[i]);
  JoystickValue[i] = map(JoystickPin, 0, 1023, 10, 110);         // the mapped value should be from 0 to 127 for true midi signal but the extreme often sound to agressive so I choose 5 to 123
  if(PreviousJoystickValue[i]!= JoystickValue[i]){               // If the Joystick has been moved
      PreviousJoystickValue[i] = JoystickValue[i];               // Backup the value of the joystick
      MIDImessage(ControlChange, i, JoystickValue[i]);           // Send the corresponding midi message to the serial port
    }
}; // End of Joysticks sensors part


} // End void loop()



```


Réalisation
=====

Voici la première version de ce contrôleur midi:

[front]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_front.jpg "midi-controller-tower - front"
![alt text][front]

[side]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_side.jpg "midi-controller-tower - side"
![alt text][side]


Annexes
=====


Circuit
======

Ci-dessousle montage électronique schématisé avec le logiciel [Fritzing](http://fritzing.org/). Je n'ai représenté qu'un capteur de chaque type par souci de lisibilité du schéma : un bouton, un capteur piezo, un joystick. Je n'ai pas trouvé le joystick 2 axes de Parallax dans les composants disponibles de Fritzing. Pour consulter le schéma de câblage exact de ce joystick, vous pouvez vous rendre sur le lien : [learn.parallax.com](http://learn.parallax.com/tutorials/language/propeller-c/propeller-c-simple-devices/joystick)

[Fritzing]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_Fritzing.jpg "midi-controller-tower - Fritzing"
![alt text][Fritzing]


[circuit]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_circuit.jpg "midi-controller-tower - circuit"
![alt text][circuit]


Découpe Laser
======

Création d'une boite de 11x11x40 cm dans Inkscape à l'aide du module TabbedBoxMaker.

[midi-controller-tower_lasercut.svg](midi-controller-tower_lasercut.svg)

[lasercut]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_Lasercut.jpg "midi-controller-tower - lasercut"
![alt text][lasercut]


Assemblage
======

[wire]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_wire.jpg "midi-controller-tower - wire"
![alt text][wire]

[back]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_back.jpg "midi-controller-tower - back"
![alt text][back]


How To
======

Pour utiliser le code ci-dessus, il faut installer le logiciel [Hairless midiserial ](http://projectgus.github.io/hairless-midiserial/)

En « serial port », sélectionner l’arduino. En midi out, il faut sélectionner le bus disponible dans votre DAW (Digital Audio Workstation).

[Hairless]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_Hairless.png "midi-controller-tower - Hairless"
![alt text][Hairless]


Dans Ableton live, il faut que les cases "Piste" et "Télec." du Bus soit sur On dans les Préférences midi.

[Ableton]: https://raw.githubusercontent.com/marieheuln/midi_controller_tower/master/images/midi-controller-tower_Ableton.png "midi-controller-tower - Ableton"
![alt text][Ableton]


Pour les utilisateurs de Windows, il faudra en plus d’[Hairless midiserial ](http://projectgus.github.io/hairless-midiserial/)
installer [LoopMidi](http://www.tobias-erichsen.de/software/loopmidi.html)

Pour que ça fonctionne , il faut surtout respecter l’ordre suivant :

  - Brancher l’arduino
  - Lancer Hairless midi serial
  - Lancer LoopMidi si besoin
  - Lancer Ableton live ou votre DAW
