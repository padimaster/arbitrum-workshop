# Cupcakes Descentralizados - Arbitrum Workshop

¡Bienvenido al Workshop de Arbitrum, donde la Blockchain Acceleration Foundation (BAF) y Arbitrum unen fuerzas para llevarte a la vanguardia de la tecnología blockchain!

En este taller, no solo aprenderás los beneficios de las aplicaciones descentralizadas, sino que también tendrás la oportunidad de desplegar tu primer contrato inteligente, ahora imagina la emoción de dar hacerlo Arbitrum, que te permite operar eficientemente a través de una de las soluciones de escalabilidad más avanzadas para Ethereum. 

Con Arbitrum, disfrutarás de transacciones rápidas y económicas, brindándote las herramientas ideales para dar vida a tus innovadoras ideas y construir el futuro.

# ¿Qué obtendrás al terminar el taller?
Al completar este taller, adquirirás habilidades clave en:

- **Aplicaciones Descentralizadas (dApps):** Entenderás cómo estas aplicaciones están cambiando industrias.
- **Contratos Inteligentes en Arbitrum:** Aprenderás a crear y desplegar Smart Contracts en la red de Arbitrum One, optimizando recursos.
- **Implementación Práctica de Blockchain:** Sabrás cómo aplicar soluciones blockchain en situaciones reales.

¡Adentrémonos en el maravilloso mundo de la tecnología blockchain!

- - -
# Antes de comenzar
Debemos contar con los siguientes requisitos:

## Desarrollo y despliegue local
- Navegador (Brave de preferencia)
- Remix IDE -> [Sitio Oficial](https://remix.ethereum.org/)

## Despliegue en la red de Arbitrum One
- Wallet ([Metamask de preferencia](https://metamask.io/download/))
- - -

# Arbitrum Workshop
Empecemos con este emocionante Workshop! Recuerda que al terminar el taller estarás participando por un **Giveaway de $40**

## Configuración del Repositorio
Cuando construyes aplicaciones descentralizadas, es esencial almacenar el código fuente en un repositorio. Esto te permite acceder a él fácilmente en el futuro y colaborar sin complicaciones si estás trabajando en equipo.

Al completar el taller, tendrás el código de tu primer Smart Contract alojado en un repositorio de GitHub. ¡Es el primer paso para desarrollar aplicaciones asombrosas!

Recuerda que para participar en el sorteo, debes compartir el enlace de tu repositorio. ¡No te lo pierdas!

### 1. Creación de cuenta en GitHub
Dirígete [Sitio Web Oficial de GitHub](https://github.com/) y haz clic en la opción de **registro**.
![image](https://github.com/padimaster/arbitrum-workshop/assets/71728367/77fc7a06-555f-49e5-90bb-b5a657309206)

Completa los campos del formulario con tus datos y ¡listo! Ya tendrás tu cuenta de GitHub creada y lista para usar.
<img width="733" alt="image" src="https://github.com/padimaster/arbitrum-workshop/assets/71728367/a0942f8e-e9a9-4afd-8b63-53913402ba6c">

### 2. Creación del repositorio en GitHub
#### 2.1. En la parte superior izquierda, junto al logo de GitHub, encontrarás un botón verde. Haz clic en él para crear tu primer repositorio.

![image](https://github.com/padimaster/arbitrum-workshop/assets/71728367/6afd93b6-5301-490c-a27a-24ed2587eefe)


#### Creación del repositorio

![image](https://github.com/padimaster/arbitrum-workshop/assets/71728367/7aada854-1727-45c9-8d89-66f50c138b2e)

#### Confirmar creación del repositorio

<img width="436" alt="image" src="https://github.com/padimaster/arbitrum-workshop/assets/71728367/5b952064-bcee-460d-ae24-56688048e8a4">

## Desarrollo del Smart Contract
¡Felicidades por llegar hasta aquí! ¡Vamos a empezar con el código!

### Remix IDE
Remix IDE es tu portal sin complicaciones hacia el emocionante mundo del desarrollo de Smart Contracts. Tanto si eres un experto como si estás dando tus primeros pasos, Remix te ofrece la plataforma perfecta para hacer realidad tus ideas en cuestión de segundos. Con Remix, el proceso de desarrollo y despliegue de tus Smart Contracts es rápido y sin complicaciones.

Además, Remix se integra sin problemas con otras herramientas, lo que te brinda la flexibilidad necesaria para trabajar como prefieras. Ya sea que estés explorando Ethereum por primera vez o perfeccionando tus habilidades, Remix es el destino definitivo para aprender y crecer en este emocionante ecosistema.

[¡Entra a Remix aquí!](https://remix.ethereum.org/)

<img width="1440" alt="image" src="https://github.com/padimaster/arbitrum-workshop/assets/71728367/eab515b7-d6eb-4554-aa44-d12cd8903c9b">

### Tu primero contrato

En el explorador de archivos, haz clic en "Crear nuevo archivo" y nómbralo como "MaquinaExpendedora.sol". Este archivo es donde pondrás el código que se ejecutará de forma automática y descentralizada en la Blockchain.

<img width="334" alt="image" src="https://github.com/padimaster/arbitrum-workshop/assets/71728367/1b79266b-35a9-4aba-b5ba-2c8308cf8c02">

En el panel de la derecha, tendrás la capacidad de modificar todos los archivos presentes en el explorador de archivos.
   
![image](https://github.com/padimaster/arbitrum-workshop/assets/71728367/fb8c791d-5ac2-450e-b600-0fba1166b937)

En el encabezado de un Smart Contract, es esencial incluir la licencia y la versión del compilador de Solidity. Aquí tienes un ejemplo:

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;
```
   
Ahora, para crear la estructura de nuestra Máquina Expendedora descentralizada, utilizaremos la palabra reservada "contract" seguida del nombre del contrato. Por convención, este nombre deberá ser el mismo que el del archivo. Con nuestro contrato sería:

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

contract MaquinaExpendedora {
    
}
```

Guardamos el registro de cupcakes de cada usuario
```solidity
// state variables = internal memory of the vending machine
    mapping(address => uint) private _cupcakeBalances;
    mapping(address => uint) private _cupcakeDistributionTimes;
```

Añadimos las reglas de la máquina expendedora
```solidity
function giveCupcakeTo(address userAddress) public returns (bool) {
        // Rule 1: The vending machine will distribute a cupcake to anyone who hasn't recently received one.
        uint fiveSecondsFromLastDistribution = _cupcakeDistributionTimes[userAddress] + 5 seconds;
        bool userCanReceiveCupcake = fiveSecondsFromLastDistribution <= block.timestamp;

        if (userCanReceiveCupcake) {
            _cupcakeBalances[userAddress]++;
            _cupcakeDistributionTimes[userAddress] = block.timestamp;
            return true;
        } else {
            revert("HTTP 429: Too Many Cupcakes (you must wait at least 5 seconds between cupcakes)");
        }
    }
```

Función para obtener el número de cupcakes de cada usuario
```solidity
 // Getter function for the cupcake balance of a user
    function getCupcakeBalanceFor(address userAddress) public view returns (uint) {
        return _cupcakeBalances[userAddress];
    }
```


