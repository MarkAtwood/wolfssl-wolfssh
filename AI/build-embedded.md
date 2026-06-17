# Building wolfssh for Embedded / RTOS

wolfssh runs on multiple embedded platforms. The `ide/` directory contains ready-made project files for each platform. All embedded builds depend on wolfSSL/wolfCrypt being present and configured for the same target.

## IDE Project Files

| Directory | Platform |
|-----------|----------|
| `ide/Espressif/` | Espressif ESP32 / ESP-IDF |
| `ide/IAR-EWARM/` | IAR Embedded Workbench for ARM |
| `ide/mplabx/` | Microchip MPLAB X |
| `ide/MQX/` | NXP MQX RTOS |
| `ide/Renesas/` | Renesas (multiple families) |
| `ide/STM32CUBE/` | STM32CubeIDE |
| `ide/winvs/` | Windows (Visual Studio) |

Each subdirectory has its own README with platform-specific setup instructions.

## Zephyr

wolfssh includes Zephyr RTOS module support. See the `zephyr/` directory at the root of the repository for Kconfig options and sample configurations. The GitHub Actions workflow `.github/workflows/zephyr.yml` shows the CI build procedure.

## Espressif (ESP32 / ESP-IDF)

Project files are in `ide/Espressif/ESP-IDF/`. Use the ESP-IDF toolchain and `idf.py` to build:

```bash
cd ide/Espressif/ESP-IDF/examples/<example>
idf.py set-target esp32
idf.py build
idf.py flash monitor
```

wolfSSL must be present as a managed component or manually added to the ESP-IDF components directory. See the `README.md` in `ide/Espressif/` for details.

## IAR Embedded Workbench

Project files are in `ide/IAR-EWARM/`. Open the `.eww` workspace file in IAR Embedded Workbench for ARM. wolfSSL must be built and referenced as a library in the project settings.

## MPLAB X (Microchip)

Project files are in `ide/mplabx/`. Open the `wolfssh.X` project in MPLAB X IDE. Requires the XC32 compiler and wolfSSL configured for the same target.

## NXP MQX

Project files are in `ide/MQX/`. See the `README.md` in that directory for MQX-specific configuration and linking instructions.

## Renesas

Project files are in `ide/Renesas/`. Multiple Renesas families are supported. See the subdirectory README files for the applicable e2 studio project setup and wolfSSL integration steps.

## STM32CubeIDE

Project files are in `ide/STM32CUBE/`. Import the project into STM32CubeIDE. wolfSSL must be configured and included as a library. See `ide/STM32CUBE/README.md` for details.

## General porting notes

- wolfssh delegates all cryptographic operations to wolfCrypt. Porting wolfssh to a new target primarily means porting wolfSSL/wolfCrypt first.
- Define `WOLFSSL_USER_SETTINGS` and provide a `user_settings.h` to configure wolfSSL features without autotools.
- wolfssh's own feature set (SFTP, SCP, etc.) is controlled by defines such as `WOLFSSH_SFTP`, `WOLFSSH_SCP`, and `WOLFSSH_SHELL`.
- Contact support@wolfssl.com for assistance porting to unlisted targets.
