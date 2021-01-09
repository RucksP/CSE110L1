



# About Myself

I am a Mathematics-Computer Science student at UCSD who is interested in working as a software engineer once I graduate.

My github can be found [here](https://github.com/RucksP)

Here is a relative link to my cat.


## My favorite block of code

When coding I like to thing of this quote from my High School Physics Teacher

> An Engineer will spend 2 weeks trying to save 5 minutes.

I think the code I've written which most exemplifies this trait when I wanted to press 1 less button on my game controller and spent **2 days** trying to make it a reality.
A  small snippet of the work I had to do can be seen here.

``` 
/** Description: checks which buttons were pressed for the designated controller
 *              at calling time
 *
 * Parameters:
 * port - the port of the controller whose inputs we want to read
 * 
 * Return: a GCC struct which contains which buttons were pressed
 *         from the controller at the assigned port
 */
struct GCC Input(int port) {

    struct GCC pad = {};

    if(adapter_handle == NULL || adapter_status == 0) {
        //return an empty pad
        return pad;
    }

    int payload_size = 0;
    uint8_t controller_payload_copy[37];

    {
        copy(controller_payload, controller_payload_copy);
        payload_size = controller_payload_size;
    }

    
    //if the transfer was incomplete
    if(payload_size != sizeof(controller_payload_copy) ||
        controller_payload_copy[0] != LIBUSB_DT_HID) {
            logs = fopen(LOGS_TXT, "a");
            fprintf(logs, "error reading payload (size: %d, type: %02x)\n", payload_size,
              controller_payload_copy[0]);
            fclose(logs);
    }

    else {
        uint8_t type = controller_payload_copy[1 + (9*port)] >> 4;
        if(type != 0 && controller_types[port] == CONTROLLER_NONE) {
            logs = fopen(LOGS_TXT, "a");
            fprintf(logs, "New device connected to Port %d of Type: %02x\n", port + 1,
                 controller_payload_copy[1 + (9 * port)]);
            fclose(logs);
        }
        
        controller_types[port] = type;

        if(controller_types[port] != CONTROLLER_NONE) {
            //this contains the values for if ABXY or the DPAD were pressed for this controller
            uint8_t b1 = controller_payload_copy[1 + (9 * port) + 1];
            //this contains the values for if LRZ or Start were pressed for this controller
            uint8_t b2 = controller_payload_copy[1 + (9 * port) + 2];
        
            if (b1 & (1 << 0))
                pad.button |= PAD_BUTTON_A;
            if (b1 & (1 << 1))
                pad.button |= PAD_BUTTON_B;
            if (b1 & (1 << 2))
                pad.button |= PAD_BUTTON_X;
            if (b1 & (1 << 3))
                pad.button |= PAD_BUTTON_Y;

            if (b1 & (1 << 4))
                pad.button |= PAD_BUTTON_LEFT;
            if (b1 & (1 << 5))
                pad.button |= PAD_BUTTON_RIGHT;
            if (b1 & (1 << 6))
                pad.button |= PAD_BUTTON_DOWN;
            if (b1 & (1 << 7))
                pad.button |= PAD_BUTTON_UP;

            if (b2 & (1 << 0))
                pad.button |= PAD_BUTTON_START;
            if (b2 & (1 << 1))
                pad.button |= PAD_TRIGGER_Z;
            if (b2 & (1 << 2))
                pad.button |= PAD_TRIGGER_R;
            if (b2 & (1 << 3))
                pad.button |= PAD_TRIGGER_L;

        }
    }
    return pad;

}
```
## Hobbies

Some of the things I do in my free time include

 - Coding
 - Rock Climbing
 - Hiking
 - Playing Video Games
   - Bastion
   - SSBM
   - Transistor
   - Pyre
 
 Some of my favorite video games include
 
 [<img src="https://static-cdn.jtvnw.net/ttv-boxart/Super%20Smash%20Bros.%20Melee.jpg" width ="250"/>](SSBM) [<img src="https://upload.wikimedia.org/wikipedia/en/4/41/Transistor_art.jpg" width ="250"/>](Transistor) [<img src="https://www.mobygames.com/images/covers/l/372094-bastion-xbox-one-front-cover.png" width ="250"/>](Bastion) [<img src="https://upload.wikimedia.org/wikipedia/en/a/ad/Pyre_cover_art.jpg" width ="250"/>](Pyre)
 
 My favorite of those 4 would certainly be _Super Smash Bros. Melee_ for the Nintendo Gamecube
 
 if I had to Rank Them in order
 
 1. SSBM
 2. Transistor
 3. Bastion
 4. Pyre
 
 

## Life Goals

Things to Do

- [x] Learn how to code
- [ ] Make amazings projects
- [ ] See the effects of my work in the world
- [ ] ~~Conquer the world~~

[Back to Top](https://github.com/RucksP/RucksP.github.io/blob/main/README.md#about-myself)

This site was built using [GitHub Pages](https://pages.github.com/)
