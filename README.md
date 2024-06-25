# STM32H7RSWorkShop-Benefit of NeoChrom Demontration

The example will guide you through creating a graphical user interface on STM32H7S78-DK which demonstrate the benefit of 
NeoChrom GPU. We will use TouchGFX designer tool to create this interface which is composed of  two icon that continously 
rotating and a button which allows to activate/deactivate NeoChrom IP.

## Prerequisites

- TouchGFX Designer 4.24.0 
- STM32H7S78-DK board

## TouchGFX Designer 4.24.0
 3 main steps will be needed :
1. Create the background and add the widgets (two texture mapper and a toggle button) 
2. Add interactions to made the texture mapper rotate and to activate/deactivate NeoChrom 
3. Compile / download and test the generated project  

## 1. create background and add the widgets 

 - Run TouchGFX Designer 4.24.0

### 1.1. Create New project targetting the STM32H7S78-DK board
  ![Start new project](./img/Create_new_DK_project.gif)
### 1.2. Add an image 
  ![Add a background image](./img/add_image.gif)
### 1.3. Select a image with the screen size (800x480)
  ![Add a background image](./img/select_background.gif)
### 1.4. Add a first texture mapper
  - Add texture mapper widget
  - Increase scale to `2.7`
  - Resize and relocate the widget 
  ![Add a background image](./img/add_texture_mapper.gif)
### 1.5. Add a second texture mapper
  - Add an other texture mapper widget
  - Increase scale to `2`
  - Resize and relocate the widget 
  ![Add a background image](./img/add_texture_mapper2.gif)
### 1.6. Add a toogle button 
  - Add a toogle button widget
  - Change the preset of this widget
  - Relocate the widget 
  ![Add a background image](./img/add_toggle_button.gif)

## 2. Add the interaction
### 2.1 Rotation fo the texture mapper 1
  - Add a new intercation 
  - Trigger : `On every N ticks`
  - Action : `Rotate the texture mapper`
  - Choose texture mapper : `textureMapper1`
  - Tick relative angle
  - Z angle :  `0.1`
  ![Add a background image](./img/rotate_texture_mapper1.gif)

### 2.2 Rotation fo the texture mapper 2
  - Add a new intercation 
  - Trigger : `On every N ticks`
  - Action : `Rotate the texture mapper`
  - Choose texture mapper : `textureMapper2`
  - Tick relative angle
  - Z angle :  `-0.1`
  ![Add a background image](./img/rotate_texture_mapper2.gif)

### 2.3 Add the activation / deactivation of NeoChrom
  - Add a new intercation 
  - Trigger : `button is clicked`
  - Action : `Execute C++ code`
  - Code : copy and paste this code 
  ```c
  #ifndef SIMULATOR
  static uint8_t b_NeoChromEnabled = 1;
    if (b_NeoChromEnabled)
    {
      b_NeoChromEnabled = 0;
       // function natively in TouchGFX for STM32H7RS
      ((TouchGFXHAL*)touchgfx::HAL::getInstance())->activateNeoChrom(false); 
    }
    else
    {
      b_NeoChromEnabled = 1;
      // function natively in TouchGFX for STM32H7RS
      ((TouchGFXHAL*)touchgfx::HAL::getInstance())->activateNeoChrom(true); 
    }
  #endif /*SIMULATOR*/
  ```
  ![Add a background image](./img/add_code.gif)

  - Include : copy and paste this code 
  ```c
    #ifndef SIMULATOR
    #include <TouchGFXHAL.hpp>
    #endif/*SIMULATOR*/
  ``` 
  ![Add a background image](./img/add_include.gif)

## 3. Compile and download to the target
  - connect STM32H7S78-DK to your PC
  - launch `Program and Run to Target`
    ![Add a background image](./img/compile_and_download.gif)
  - Result on the target    
    ![Add a background image](./img/demo_result.gif)

