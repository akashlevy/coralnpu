# CoralNPU simulation with dsim

## Prereqs: 
1. Docker available.
2. Put `AltairDSim2025.0.1_linux64.bin` and `dsim-license.json` into `dsim/`.
3. Clone coralnpu-mpact repo in the same path as this repo (otherwise, update CORALNPU_MPACT in Makefile)

## Build images
```
cd dsim
docker build --platform linux/amd64 -t dsim .
cd ..
docker build --platform linux/amd64 -f utils/coralnpu.dockerfile -t coralnpu .
```

## Launch container
`docker run -it --platform linux/amd64 -v $(pwd):/workspace -w /workspace coralnpu`

## Compile UVM testbench (inside container)
`cd tests/uvm`
`make compile`

## Provide program ELF
Copy your ELF into `tests/uvm/bin`

## Run a test
`make run TEST_ELF=./bin/<test_elf_filename>`

## Outputs
- Logs: `sim_work/logs/`
- Waves: `sim_work/waves/`
