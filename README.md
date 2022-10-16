# cube2-quake
> cube2 fork with quake like strafe-jumping (air acceleration) mechanics

## Implementation
Quake 3 style circle walk and strafe jumping bonus implemented within the main physics routine for updating the velocities, based on this [commit](https://github.com/id-Software/Quake-III-Arena/blob/dbe4ddb10315479fc00086f08e25d968b4b43c49/code/game/bg_pmove.c#L240).

```c
  float nostrafebonus = pl->move && !pl->strafe ? 1.3f : 1.0f;
  float fallslidebonus = pl->physstate < PHYS_SLOPE ? 1.3f : 1.0f;
  d.mul(nostrafebonus * fallslidebonus);

  float maxspeed = pl->maxspeed * nostrafebonus * fallslidebonus;
  vec playervel = vec(pl->vel.x, pl->vel.y, 0);
  float projspeed = playervel.dot2(m);
  float addspeed = clamp(maxspeed-projspeed, 0.0f, maxspeed);

  // circle move bonus scales up the player's inputs
  vec circlemovebonus = vec(m).mul(addspeed*circlemoveaccel);
  d.add(circlemovebonus);
  
  if(pl->physstate==PHYS_FALL && pl->strafe && (!strafejumprequiremovekey || pl->move))
    {
       // strafe jumping bonus scales up the player's existing velocity
       vec strafejumpbonus = m.mul(addspeed*strafejumpaccel);
       d = playervel.add(strafejumpbonus); // override d entirely
       if(strafejumpwithcirclemovebonus) d.add(circlemovebonus);
    }
```     
   
## Installation

**No binaries are provided.** Therefore, you must build this project from
sources to run it.

- Clone this repository
- Copy or symlink the `packages/` folder from your
  [Cube 2: Sauerbraten](http://sauerbraten.org) installation.
  (This must done because `packages/` can't legally be redistributed
  in modified versions of the game.)
- Compile a client and server binary. On Linux, run `make -C src install` in a terminal while in
  the root folder of the cloned repository.
- Run the game with `./sauerbraten_unix` in the root folder.

## License

Copyright © 2001-2020 Wouter van Oortmerssen, Lee Salzman, Mike Dysart, Robert Pointon, and Quinton Reeves

Mod changes © 2020-2022 Hugo Locurcio

Licensed under the Zlib license, see [LICENSE.txt](src/readme_source.txt) for details.
