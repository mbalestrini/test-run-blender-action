# test-run-blender-action

Repository to test the run-blender-action: https://github.com/mbalestrini/run-blender-action

main.yaml call to `run-blender-action`:
```
      - name: Start the blender docker
        id: blender_docker
        uses: mbalestrini/run-blender-action@master
        with:
          file-to-load: TEMPLATE_SKY130_LIBRARY_CELLS.blend
          blender-extra-args: -P ./scripts/library_cell_render.py -- -i ./src_files/sky130_fd_sc_hd__mux2_1.json -o ./generated-renders/ -s 1.0
```

This job executes blender from the command line with the following parameters:

`blender TEMPLATE_SKY130_LIBRARY_CELLS.blend -P ./scripts/library_cell_render.py -- -i ./src_files/sky130_fd_sc_hd__mux2_1.json -o ./generated-renders/ -s 1.0`

After finishng the render the job uploads the files as an artifact to be able to download them from the action:
```
      - name: Upload render output as artifact
        uses: actions/upload-artifact@v2
        with:
                name: renderer-files
                path: ./generated-renders/*.jpg
```

Then it commits and pushes the rendered file to this repository




