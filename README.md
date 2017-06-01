# KSwe SoSe 2017 - Aufgabe 6

In dieser Aufgabe soll entweder die Javascript-Anwendung für Messstationen
erweitert oder alternativ eine Android-App entwickelt werden.

Die Anwendung soll folgende Funktionalität erweitert werden bzw. bereitstellen:

* Abonnieren von Echtzeit-Messdaten mit Hilfe von MQTT
* Aktualisierung des Zeitreihen-Diagramms bei Empfang neuer Messwerte

## Daten

Es soll die folgende REST API als Datengrundlage genutzt werden:

https://kswe2017.daplie.me/api

Eine Kurzdokumentation der API steht unter folgender URL zur Verfügung:

https://kswe2017.daplie.me/docs/

## Ergebnis

Die Anwendung soll die REST API nutzen, um die Grunddaten der Stationen zu beziehen.
Die Echtzeit-Daten sollen dann - via MQTT bezogen - in der Anwendung visualisiert
werden.


## MQTT-Broker

*Infos im Trello-Board*

## MQTT-Bibliotheken

[Eclipse Paho](https://eclipse.org/paho/) stellt Bibliotheken für viele
Programmiersprachen und Plattformen bereit (Java, Javascript, Python, Android, ...).

### Android

Das Paho-Projekt stellt einen Android-Service bereit, der direkt genutzt werden
kann. Es sind einige Einträge in der `AndroidManifest.xml` nötig (Permissions und
Service):

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="matthes.kswe.fbg.hsbochum.de.mqtt_android">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application>
        ...

        <service android:name="org.eclipse.paho.android.service.MqttService">
        </service>
    </application>

</manifest>
```

In den `dependencies` der `build.gradle` des Modules muss die Bibliothek eingebunden:

```
compile 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.1.0'
compile 'org.eclipse.paho:org.eclipse.paho.android.service:1.1.1'
```

Zusätzlich muss noch das Paho-Repository eingebunden werden (oberste Ebene der
`build.gradle`):

```
repositories {
    maven {
        url "https://repo.eclipse.org/content/repositories/paho-releases/"
    }
}
```
