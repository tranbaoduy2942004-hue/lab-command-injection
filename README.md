# Command Injection & SOC Investigation

A lightweight, standalone Labtainer cybersecurity training lab.

## Architecture

Three Docker containers:

- Attacker: OS Command Injection simulation
- WebApp: Intentionally vulnerable Python web application
- SOC: Event collection, correlation and investigation

## Attack Chain

1. Legitimate diagnostic request
2. OS Command Injection using a shell command separator
3. Server-side command execution
4. Access to a simulated data record
5. SOC detection and investigation

Only synthetic training data is used.

## Requirements

- Labtainer VM with Docker
- Internet connection for initial image download

## Installation

On a Labtainer VM:

    imodule https://raw.githubusercontent.com/tranbaoduy2942004-hue/lab-command-injection/main/imodule.tar

    labtainer lab-command-injection

## Run Simulation

Use another terminal on the Labtainer host.

Start SOC:

    docker exec -d -u ubuntu -e HOME=/home/ubuntu lab-command-injection.soc.student lab11-soc

Start WebApp:

    docker exec -d -u ubuntu -e HOME=/home/ubuntu lab-command-injection.webapp.student lab11-web

Allow the services to start:

    sleep 2

Run the attack:

    docker exec -u ubuntu -e HOME=/home/ubuntu lab-command-injection.attacker.student lab11-attack

Run SOC investigation:

    docker exec -u ubuntu -e HOME=/home/ubuntu lab-command-injection.soc.student lab11-soc --detect

View investigation evidence:

    docker exec -u ubuntu -e HOME=/home/ubuntu lab-command-injection.soc.student cat /home/ubuntu/lab11/investigation.json

Grade the lab:

    checkwork lab-command-injection

If a service is not ready, verify that it is listening before
retrying the simulation.

## Expected Outcomes

- BASELINE_OK
- COMMAND_INJECTION_OK
- DEMO_DATA_READ_OK
- LAB11_ATTACK_OK
- LAB11_SOC_OK
- VERDICT=true_positive

## Assessment

6 auto-graded objectives.

Development Labtainer VM: 6/6 PASS.

## Docker Hub

Publisher: tranbaoduy

## Security

The web application is intentionally vulnerable.
Run only within the isolated Labtainer environment.
Do not expose its HTTP service to untrusted networks.

## Compatibility

Public IModule download and clean VM grading must be
independently verified.

## Labtainer Image Compatibility

Docker Hub images include Labtainer base-image metadata.

The lab uses:

    BASE_REGISTRY labtainers

The development VM successfully started all three containers
and passed the six grading objectives.

Independent clean-VM installation remains to be verified.
