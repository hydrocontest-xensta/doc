# Micro-controleurs

Référence de nos modèles:
`STM32-L476RG` (gamme `Nucleo-64`)

## Outils de développement

### IDE

### CubeMX

CubeMX est un outil de génération de code pour commencer un projet.

A partir du modèle de la carte choisie, on peut configurer les fonctions des différents pins, mettre en place des interruptions, l'OS FreeRTOS, des Timers, etc. Tout n'est pas forcément hyper clair, mais en suivant des tutos on se débrouille.

Le logiciel génère ensuite un dossier de projet complet que l'on peut modifier, compiler et envoyer sur la carte. 



[Lien vers la page de téléchargement](https://www.st.com/en/development-tools/stm32cubemx.html)

#### Modifier un projet déjà généré

CubeMX peut modifier un projet généré sans écrasé votre code si vous avez placé celui-ci:

- soit dans les balises dédiées (voir extrait plus bas)
- soit dans des fichiers différents: dans ce cas il faudra modifier le fichier de projet/Makefile après regénération

Les balises de code se présentent comme suit, il faut insérer son code entre `XX BEGIN` et `XX END`

```c
/**
 * @brief USART1 Initialization Function
 * @param None
 * @retval None
 */
static void
MX_USART1_UART_Init(void)
{

  /* USER CODE BEGIN USART1_Init 0 */
  char code_perso[] = "ici je peux mettre du code"
  /* USER CODE END USART1_Init 0 */

  /* USER CODE BEGIN USART1_Init 1 */
  int code_perso_ici_aussi = 42;
  /* USER CODE END USART1_Init 1 */
  huart1.Instance = USART1;
  huart1.Init.BaudRate = 115200;
  huart1.Init.WordLength = UART_WORDLENGTH_8B;
  huart1.Init.StopBits = UART_STOPBITS_1;
  huart1.Init.Parity = UART_PARITY_NONE;
  huart1.Init.Mode = UART_MODE_RX;
  huart1.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart1.Init.OverSampling = UART_OVERSAMPLING_16;
  huart1.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE;
  huart1.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT;
  if (HAL_UART_Init(&huart1) != HAL_OK) {
    Error_Handler();
  }
  /* USER CODE BEGIN USART1_Init 2 */
  appeler_ma_fonction(&huart1, code_perso);
  /* USER CODE END USART1_Init 2 */
}
```

## Formation

Ces cartes sont assez complexes à programmer, pensez à vous former sur les sujets suivants:

- interruptions systèmes
- OS temps réel : multitastking, scheduling...

et quelques plus (utilisables pour des fonctions avancées)

- DMA

### Tutoriels

Pour commencer, quelques tutos supers qui donnent les bases sur CubeMX en même temps: [https://simonmartin.ch/resources/stm32/dl/](https://simonmartin.ch/resources/stm32/dl/)