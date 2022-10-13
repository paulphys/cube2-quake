# cube2-quake
> cube2 fork with quake like strafe-jumping (air acceleration) mechanics

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
