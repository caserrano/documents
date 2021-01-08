# Protocolo de intercambio automático (Perpetual Swap) basado en AMM (creadores de mercado automáticos)

## 1. Introducción

El Protocolo Mai V3 diseñado por MCDEX es un creador de Mercado automatizado (AMM) basado en la permuta continua de protocolos descentralizados (Perpetual Swap)
Este tipo de contrato es uno de los derivados financieros más populares puesto que no tiene fecha de caducidad, admite el trading de alta frecuencia y mantiene su precio vinculado al precio del índice.
 

El objetivo de este protocolo es permitir que cualquiera pueda crear y comerciar en cualquier mercado perpetuo. Sin ir más lejos, cualquiera puede crear su propio mercado perpetuo o de permuta financiera con el precio del activo subyacente y elegir entre los distintos tokens ERC 20 como garantía o colateral. En segundo lugar, hemos diseñado el AMM o creador de Mercado automatizado correspondiente al Mercado de permuta financiera, dotando al AMM de mayor capitalización y eficiencia. De la misma forma, el Mercado automatizado vendría a solucionar el problema de baja liquidez.
Cualquier usuario puede proveer de liquidez  a cualquier Mercado automatizado depositando sus activos en una piscina o pool y generar por consiguiente ganancias de mercado razonables.
Por último cualquiera puede realizar Perpetual Swaps en total libertad y de una forma absolutamente descentralizada. Los activos de los comerciantes o traders están integrados en los contratos inteligentes manteniendo en todo momento su custodia, de esta misma forma garantizando que los procesos de trading se realicen completamente dentro de la cadena principal y legítima. 

El contrato inteligente del protocolo está estrictamente auditado por terceras personas neutrales además de no disponer de la administración clave del protocolo, maximizando de esta forma la  descentralización y la seguridad del protocolo.

Creemos que la clave principal del protocolo es que es totalmente abierto y descentralizado, enfocado a que el poder recaiga principalmente en la comunidad que apoya y contribuye con el ecosistema de MCDEX. Cualquier usuario podría crear un Mercado de permuta financiero con activos sintéticos ya sea en la cadena principal o en la red de pruebas conocida como testnet. Conforme crezca el desarrollo de la comunidad de MCDEX se generará inevitablemente más mercados de  permutas, generando por consiguiente mayor volumen de Mercado

## 2.  Mercados de permutas financieras (Perpetual Swaps)

### 2.1 participantes del mercado
Este protocolo está basado completamente en el AMM. Por favor referirse al diseño MAI V3 AMM documento con información detallada en todo lo referente al AMM

El Mercado presenta los siguientes roles: 

#### AMM (Creador de Mercado Automatico)

AMM: Es el actor principal de contrapartida proporcionando liquidez al Perpetual Swap. Como un trader común, AMM presenta su cuenta marginal independiente y tiene la cualidad de aguantar posiciones de mercado.

#### Operador

El operador en este caso es el creador y administrador del Perpetual Swap 
- Pasos para convertirse en operador:
  - Crear el Perpetual Swap y configurar los parámetros iniciales como la proporción marginal de trading, los parámetros de riesgo del AMM etc. El AMM of the Perpetual Swap incluye de entrada parámetros de riesgo. Al ajustar dichos parámetros, el operador tiene la facultad de cambiar el riesgo de mercado del AMM, la profundidad del mercado, incongruencias o propagación de desvíos etc.
  - Pague (o proporcione) el servicio de oráculo. El protocolo define una interfaz de oráculos para que dichos oráculos ya definidos se puedan aplicar en este protocolo. Un operador también puede proporcionar sus propios datos obtenidos del oráculo a las permutas financieras. 
  - Un operador puede establecer un rango de parámetros de riesgo y ajustar estos dentro del mismo rango. 
  - Un operador puede iniciar el proceso de gobernanza para cambiar el nivel de los parámetros de riesgo. (ver 2.10 parámetros y gobernanza de AMM)
  - El operador puede transferir su función a otras direcciones y excluir su función de operador. El mercado perpetuo  sin operador estará regido por proveedores de liquidez (LP).
  
- Beneficios:
  - Benefíciese de cada operación cobrando una tarifa de gestión establecida por ellos mismos 
  - Los incentivos se han de  distribuir potencialmente a piscinas de inversión que arrojen buenos resultados.
  - iniciar propuesta de gobernanza AMM.

- Riesgos: No aplicable 

#### Proveedor de liquidez:
- Cómo convertirse en proveedor de liquidez
  - Depositar el colateral o garantía en la pool de Mercado automatizado
- Beneficios:
	- Operaciones con comisiones fijas
	- Benefícios en lo referente a la fluctuación del precio y sus discrepancias
	- El trader se hace cargo de los pagos de financiación
	- Sanción por liquidación
	- El incentivo se distribuirá potencialmente entre pools de AMM (consulte la sección 3.2 tokenomics)
	- Los proveedores de liquidez pueden participar en la gobernanza de AMM (consulte la sección 2.10 Los parámetros y Gobernanza de AMM).
	
- Riesgos:
  - Cuando el AMM mantiene una posición,  este está expuesto a un factor de riesgo, si el índice del precio cambia en ese momento, podría podría generar pérdidas al AMM. En este caso estas pérdidas potenciales serán compartidas por todos los proveedores de liquidez. 

#### Trader:
Los traders forman la mayor parte del mercado. Los operantes llevan  a cabo la cuenta de ganancias y pérdidas (P & L) comerciando contra AMM siendo estos  siempre los beneficiarios. En este protocolo, todas las operaciones deben pasar por AMM, en este caso ninguno de los traders puede pasar por alto el AMM y generar trading entre ellos mismos. Para cada operación, los comerciantes deben pagar una cierta cantidad de tarifa de transacción. Además, el comerciante pagará o recibirá el pago de la financiación de acuerdo con la política de tasas de financiamiento.

#### Guardián:
Guardián es una función auxiliar. Cualquiera puede ser un guardián para liquidar cuentas con margen insuficiente (ver sección 2.4 liquidación).

#### Delegado:
El rol de delegado es un caso especial puesto que podría haber un delegado para cada  cuenta de margen. Un delegado puede operar sobre la cuenta para comerciar (bien sea a través o directamente contra el AMM o mediante un broker), sin embargo estos no pueden retirar fondos de la cuenta bajo ningún motivo. El objetivo en particular del delegado es separar las billeteras frías y calientes y llevar a cabo la custodia de las estrategias comerciales. 

### 2.2 pago de financiación:
Al igual que con el intercambio perpetuo tradicional o Perpetual Swap, este protocolo utiliza el pago de financiación para anclar el precio del índice.
Dado que todas las operaciones deben pasar por AMM, el mercado alcanza el equilibrio cuando el AMM no mantiene ninguna posición. En este punto, el AMM proporcionará la mejor oferta y el mejor precio de demanda alrededor del índice, manteniendo así el precio de mercado actual cercano al índice.
El precio de AMM fluctúa según su posición. Cuando el AMM tiene posiciones largas, el precio de de este será más bajo que el precio del índice y viceversa, cuando  el AMM adquiere posiciones en corto. Dicho de otra forma, el mercado se encuentra desbalanceado en este punto, por lo tanto, el precio de mercado cambiará en relación con el índice. En este caso, el protocolo efectuará el cobro del pago de financiación de las posiciones en contra del AMM, en cuanto a los traders con posiciones a favor del AMM, estos terminaran recibiendo el pago de la financiación. Por consiguiente, el AMM recibe el pago de la financiación siempre y cuando mantenga posiciones de trade. La tasa de financiación se correlaciona positivamente con el tamaño de la posición del AMM, es decir, cuantas más posiciones tiene el AMM, más se desvía el precio de mercado, lo que provoca un pago de financiación más alto.
Por un lado, el pago de financiación puede evitar que más traders se conviertan en contrapartes del AMM, algo que podría provocar una mayor desviación de precios. Por otro lado, una tasa más alta de financiamiento atraerá más proveedores de liquidez y por consiguiente más fondos a la hora de abrir una posición con AMM. Además, basado en el diseño del AMM, tanto la agregación de liquidez como la negociación en corto del AMM, condición  que reduce el tamaño de la posición de AMM, facilitarán la disminución en la desviación estándar de precios. En conclusión, el pago de la financiación hará que el precio de mercado vuelva al índice.


### 2.3 Margen de ganancias y pérdidas (P&L)
Debido a la naturaleza abierta y sin permisos de este protocolo, cualquiera puede crear intercambios perpetuos con diferentes niveles de riesgo. Para evitar la propagación del riesgo entre diferentes intercambios perpetuos o perpetual swaps, el protocolo utiliza un mecanismo de margen aislado: En síntesis cada uno de los perpetual swaps de cada trader tiene su propia cuenta de margen independiente, además el margen de ganancias y beneficios de la cuenta no le afectara  bajo ninguna medida a otras cuentas de margen que los traders puedan abrir y o negociar

Cuando un trader se posiciona en largo o en corto sobre un `ΔN` contratos a un precio de entrada determinado `P_entry`, `ΔN>0` indica que el trader se posiciona en largo, `ΔN<0` indica que el trader toma una posición o posiciones en corto. 

Al abrir la posición, el saldo margen de la cuenta de margen del trader en este caso debe ser mayor que o igual al margen inicial:

     P_mark·|ΔN|·R_im

P_mark marca el  precio  proporcionado por el oráculo. `P_mark` suele ser igual al precio índice `P_index` O es  un resultado TWAP de `P_index` cuando se utiliza algún oráculo descentralizado como  por ejemplo Uniswap.  `M_im` es la tasa inicial del margen del perpetual swap

La Pérdidas y Ganancias o P&L de la posición se calcularía del siguiente modo:

    (P_mark-P_entry)·ΔN	
  
En cualquier momento  se puede retirar el beneficio de la posición perpetua de MCDEX, es decir, "P & L" siempre se refiere a su estado natural, mientras que la pérdida de posición se deduce del saldo margen en tiempo real.

El trader puede cerrar la posición a un precio de salida 𝑃𝑒𝑥𝑖𝑡. El P&L después de que el trader cierra su posición es:

    (P_exit-P_entry)·ΔN	

El trader debe asegurarse de que el balance de la cuenta de margen siempre sea mayor o igual que el margen de mantenimiento:

    P_mark·ΔN·M_mm

Si no se puede cumplir con el requisito básico del margen de mantenimiento, la posición se liquidará automáticamente

Al final, cada Perpetual Swap tiene un parámetro de "Recompensa como guardián del gas". Cuando se liquida una posición, el poseedor recibirá una cantidad fija en calidad de recompensa para pagar el gas. Por lo tanto, nuestro protocolo requiere que, siempre que el tamaño de la posición de la cuenta de margen sea mayor que 0 (sin tener en cuenta el valor de la posición), el balance del margen debe ser suficiente para efectuar la “Recompensa del guardián del gas”. De no ser así, la posición se liquidará. 

### 2.4 liquidación
Cuando el balance de la cuenta de margen es menor que el margen de mantenimiento, la posición se liquidará. El guardián inicia la liquidación contra posiciones que muestran márgenes insuficientes. Cualquiera puede actuar como guardián. Hay dos formas de liquidación:

- Liquidación a través del AMM: La posición liquidada se cerrará a través de AMM, lo que significa que esta posición se ha de transferir al AMM. La sanción por liquidación también se destinará a la piscina de liquidez de AMM. El guardián recibirá una cierta cantidad en calidad de recompensa como guardián de gas.
- Control asumido por el guardián: La posición liquidada se transferirá al guardián. En este caso, el guardián asume el riesgo de la posición y recibe a cambio los fondos subyacentes de la liquidación.

### 2.5 Convenio

Si bien se trata de un Perpetual Swap , podría llegar a existir una deficiencia de liquidez en situaciones extremas. Si existe una pérdida por liquidación debido a la deficiencia de liquidez del AMM o retrasos de liquidación, el fondo de seguro en el AMM dará prioridad inmediata a la recuperación de la pérdida de liquidación. Si el fondo de seguro de AMM es insuficiente, el contrato entrará en la fase de liquidación. El Perpetual Swap se liquidará al último índice del precio y el activo restante se distribuirá a los traders restantes de acuerdo con su balance de margen. Es decir, la pérdida por liquidación la asumen todos los operadores que mantienen posiciones en función de su balance de margen. Para aquellos que no tienen ninguna posición, no se les imputará ninguna pérdida por liquidación. Creemos que, en circunstancias extremas, crear un convenio puntual permitirá que los traders retiren sus márgenes protegerá indudablemente a todas las partes. Este mecanismo es una forma de solventar emergencias.

Además, cuando el oráculo deja de proporcionar actualizaciones durante más de 24 horas, el contrato también entrará automáticamente en liquidación.

Hay dos etapas de convenio. El primero se llama "Emergencia", en el cual el oráculo deja de actualizarse. En este punto, los guardianes revisarán todas las cuentas de margen y obtendrán el “Keeper Gas Reward” el gas de recompensa del guardián. Durante la revisión, el balance del margen se calculará en función del precio de liquidación. Cuando se lleve a cabo completamente la revisión, el convenio entra en una segunda etapa denominada "Aclarado". Una vez sucede esto, los traders pueden retirar el margen restante.

### 2.6 Fondo asegurador

Cada Perpetual Swap tiene integrado un fondo asegurador para pagar las pérdidas  de liquidación.

Cualquiera puede realizar donaciones al fondo asegurador. Alentamos a los usuarios a donar al capital inicial y a complementar el fondo del seguro a medida que se ejecuta el contrato. 

Cuando la posición del operador se liquida debido a un margen insuficiente, una cierta proporción (basada en los parámetros AMM) de la penalización por liquidación a cobrar se destinará al fondo asegurador. La parte restante va al liquidador (AMM o guardián). Cada fondo asegurador tiene un tope máximo de fondos. Cuando se alcanza este tope máximo, el fondo recién agregado pasa al fondo de liquidez de AMM. Un proveedor de liquidez puede aumentar este límite superior a través de la gobernanza, pero nunca se podrá reducir.

### 2.7 Órdenes de venta y órdenes límite

Negociar contra el AMM es similar a colocar una orden tradicional de mercado en el libro de órdenes tradicional. En el caso de los Perpetual Swaps, los traders suelen estar inclinados a buscar oportunidades y controlar el precio de ejecución mediante órdenes limitadas. Además, la orden de venta es una herramienta importante para operaciones con alto apalancamiento. Por lo tanto, diseñamos órdenes límite y de venta relativamente centralizadas. El trader de esta forma, puede firmar una orden límite o de venta y enviar la orden a un servidor de confianza o "Broker” El servidor broker observará el precio del AMM en la cadena y enviará la orden al contrato cuando el precio del AMM cumpla con el requisito de la orden. Cuando el contrato inteligente reciba una orden del Broker, este procederá a ejecutar la orden después de verificar su validez.

Se ha de tener en cuenta que el broker no coincidirá con las órdenes recibidas, por lo cual,  todas las órdenes se negociarán directamente contra el AMM serán ejecutadas en orden de antigüedad, es decir las primeras serán ejecutadas antes. Además el broker cobrará a los traders la tarifa de gas.

### 2.8 Seguridad

Entendemos perfectamente que la seguridad es el factor clave de este tipo de protocolos. Cabe recordar que antes de ser publicados, todos los contratos y actualizaciones pasarán por una estricta auditoría. Además también se verificará el diseño de la estructura financiera del AMM.
Por último para maximizar la característica descentralizada de este protocolo, no hay una clave de administración en el código. 

Por último para maximizar la característica descentralizada de este protocolo, no hay una clave de administración en el código. 

Aunque los operadores tienen privilegios limitados sobre los Perpetual Swaps, que hasta cierto punto aumentan la seguridad del protocolo, los traders han de elegir cuidadosamente los Perpetual Swaps que les gustaría negociar y operar estrictamente bajo su propio riesgo. Alentamos a los operadores a elegir oráculos descentralizados y limitar así los parámetros de riesgo a un rango más pequeño (o establecer parámetros fijos), de modo que se pueda aumentar la credibilidad.

### 2.9 Remitente

Este protocolo admite comisiones de referidos. El remitente recibirá una cierta comisión derivada de las tarifas de los trades y proveedores de liquidez cuando el arbitraje de estos negocie contra el AMM o mediante un broker. La proporción de esta tarifa remitida será establecida por la gobernanza del AMM. De esta manera, los inversores institucionales pueden beneficiarse de recomendar  traders al AMM ejecutando de esta forma, su propia interfaz.

### 2.10 Parámetros y gobernanza del AMM

Los parámetros del AMM presentan dos categorías: los modificables y los inalterables. El operador y el proveedor de liquidez pueden ajustar los parámetros modificables votando. El AMM tiene un grupo de parámetros de riesgo y cada uno tiene un nivel efectivo. Según el mercado, el operador puede ajustar libremente los parámetros de riesgo dentro del rango efectivo. Para realizar cambios en el rango si es necesario, se ha de recurrir a un procedimiento de votación.

Un operador puede iniciar una propuesta. Siempre y cuando no haya un operador en el Perpetual Swap, también puede iniciar la propuesta los proveedores de liquidez con una participación superior al 1%. Cada propuesta procederá por votación entre los proveedores de liquidez que posean el token adjudicado a estos antes de que se inicie la propuesta. El quórum de votos debe ser superior al 10% del total de los activos del proveedor de liquidez. El período de votación dura 72 horas y la resolución puede entrar en vigencia después de un periodo de 24 horas. Al votar, los proveedores de liquidez han de depositar sus tokens de liquidez. Si se aprueba la propuesta, entonces el token de los proveedores de liquidez que votaron sí se desbloquearán automáticamente después de 72 horas desde la ejecución de la propuesta; el token de liquidez de los liquidity providers que votaron no se desbloqueará inmediatamente. Si la propuesta falla, entonces todos los tokens de los proveedores de liquidez se desbloquearán inmediatamente después del período de votación. Cuando un proveedor de liquidez inicia una propuesta, el sistema registra automáticamente su voto como "sí" y bloqueará su token de liquidez. 

| Parametros deAMM | Definicion | Alterable/Inalterable |
|------------------|------------|-----------------------|
|Activo subyacente | Una cadena que identifica el activo subyacente.| Inalterable |
|Dirección del token colateral|	Dirección del colateral ERC 20 token | Inalterable |
|Dirección del operador | La dirección propia del operador | Alterable por el operador|
|Dirección del adaptador del oráculo | La dirección del adaptador es compatible con el oráculo Mai3 | Inalterable |
|ITasa de margen inicial | Determina el apalancamiento máximo en el momento de abrir la posición | Alterable por la gobernanza de los proveedores de liquidez (solo se permite disminuciones)|
|Tasa de mantenimiento del margen | Determina el apalancamiento cuando se liquida la posición; Más pequeño que la tasa de margen inicial | Alterable por la gobernanza de los proveedores de liquidez (solo se permite disminuciones)|
|Tarifa de la bóveda | La tasa de comisiones de trading que ingresan en la DAO bóveda |	Alterable por la gobernanza de MCDEX DAO |
|Tarifa de operador | The rate of trading fee that goes to operator; Less than 1%|	Alterable by LP Governance|
|LP Fee|	The rate of trading fee that goes to LP; Less than 1%|	Alterable by LP Governance|
|Referral Fee|	The rate of referral fee from the Operator Fee and LP Fee|	Alterable by LP Governance|
|Liquidation Penalty Rate|	The rate of liquidation penalty. Liquidation Penalty=Position Value* Liquidation Penalty; Smaller than the maintenance margin rate|	Alterable by LP Governance|
|Insurance Fund Rate|	The ratio of penalty that goes to the insurance fund|	Alterable by LP Governance|
|Insurance Fund Max|	The upper limit of the insurance fund|	Alterable by LP Governance (only increments are allowed)|
|Keeper Gas Reward|	When keeper executes liquidation or reviews accounts during settlement, they receive a fixed amount of reward to pay for Gas.|	Alterable by LP Governance|
|AMM Risk Parameters|	A set of parameters that helps with the risk management of AMM as the market maker|	The Effective Range is Alterable by Governance, and Operator Adjusts within Range.|


Please pay attention to the fact that all the risk parameters are effective within a designated range. Operators can adjust the parameters within this range without going through the governance procedures. In such way, LP can authorize the operator adjust the risk parameters according to the market, which is significant at an early stage. After the protocol has been running for a while and the risk parameters gradually stabilize, LP can cut the effective range of the risk parameters through governance (or even fix the parameters) to further strengthen AMM’s decentralized characteristic. 

In addition to the proposals for revising AMM parameters, there are three special proposals that requires a vote quorum no less than 20% of the total LP share.
  - Upgrade the code of AMM smart contract
  - Make a perpetual swap enter settlement stage
  - Appoint an operator. LP can initiate this proposal only when there is no operator.
  
### 2.11 Multi-chain deployment

MCDEX believes that various public chains have their own users and ecosystems. This protocol stays neutral when choosing public chains. In order to maximize our usability, the smart contracts of this protocol are able to run on various public chains. MCDEX DAO will support the development of this protocol on these public chains, growing the MCDEX ecosystem. 

## 3. MCDEX DAO

### 3.1 Governance 

The MCDEX community has issued its governance token MCB and has done a series of governance work. While launching the Mai3 protocol, we will establish MCDEX DAO based on MCB. MCDEX DAO will be the core of the MCDEX community. The mission of MCDAO is to continuously develop the MCDEX ecosystem. 

MCDEX DAO has vault. The asset in this vault comes from: 
  - Share from the fee captured by MCDEX ecosystem
  - Newly issued MCB in the MCB tokenomics
  - Other payments made to MCDEX DAO
  
The asset in the vault is used to assist the MCDEX DAO mission. Its specific usage includes but not limited to:
  - Liquidity incentive: Incentives for LP of AMM
  - Governance incentive: Incentives for MCB holders who participate in community governance
  - Development incentive: Incentives for community starters and community managers
  - Audit fee and other required fee
  - Add liquidity to products in the MCDEX ecosystem
  - Buyback MCB from the secondary market. The MCB will be part of the vault asset
  - Provide liquidity for MCB (in the MCB liquidity pool on Uniswap)

MCB holders have the governance right of MCDEX DAO. MCDEX DAO applies the “Off-chain discussion, On-chain governance” method. Since the governance is on the chain, every proposal is essentially an executable smart contract. MCDEX DAO should provide a smart contract factory for the ease of initiating proposals. 

The MCDEX DAO governance includes:
  - Managing the specific usage of the vault asset;
  - Running numerous perpetual swaps as operator;
  - Electing a multi-signature address when necessary. This multi-signature address will complete the routine work representing MCDEX DAO as an operator;
  - Upgrading MCDEX DAO smart contract

The MCDEX governance proposal needs to be initiated by MCB holders, and the initiator’s MCB voting power has to be no less than 1% of the issued total. The voting quorum has to be no less than 10% of the issued total. The proposal initiator is set to vote yes. 

A MCB holder can delegate the voting power to another holder.

The voting period lasts 72 hours, and there is a time lock of 48 hours. Participants need to stake MCB. If the proposal passes, the MCB that voted yes will be unlocked after 72 hours since the execution of this proposal, and the MCB that voted no will be unlocked immediately when the voting period terminates. If the proposal fails, all staked MCB will be unlocked immediately when the voting period terminates.

### 3.2 Tokenomics

The original MCB tokenomics has room for improvement: The rapidly increasing inflation has been overwhelming for MCB holders. Therefore, we will openly discuss the upgraded MCB tokenomics with the community before the launching of Mai 3. The tokenomics include issue size, issue object, and issue speed. 

The principles of the new tokenomics as follows: 
  - The issued MCB keeps circulating.
  - MCB has to be captured from the MCDEX ecosystem
  - Due to the significance of liquidity in derivatives, we still need to issue more MCB as liquidity incentives. 
  - The new tokenomics has to take into account the profit of current MCB holders. 

