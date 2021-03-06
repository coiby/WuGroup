Following [Download and install — Phonopy v.1.11.0](https://atztogo.github.io/phonopy/install.html)

First install requisite packages on different nodes. For details, check [Batch-install packages on all nodes from server node](miscellaneous_tips.md).

```sh
yum install numpy python-devel python-matplotlib python-yaml
```

1. Download the package from  [phonopy - Browse \/phonopy\/phonopy-1.10 at SourceForge.net](https://sourceforge.net/projects/phonopy/files/phonopy/phonopy-1.10/)
2. Extract package
  ```
  tar xvfz phonopy-1.11.0.tar.gz
  cd phonopy-1.11.0
  ```

3. Install
  ```
  python setup.py install --home=~/phonopy
  ```

4. Put `lib/python` path into $PYTHONPATH, e.g., in your .bashrc,
  ```
  export PYTHONPATH=~/phonopy/lib64/python
  ```

5. Run example Si-pwscf
  ```sh
  cd phonopy-1.11.0/example/Si-pwscf
  ~/phonopy/bin/phonopy --pwscf -c Si.in -d --dim="2 2 2"
  ~/phonopy/bin/phonopy --pwscf -f supercell-001.out;;;
  ~/phonopy/bin/phonopy --pwscf -c Si.in -p --dim="2 2 2" --pa="0 1/2 1/2 1/2 0 1/2 1/2 1/2 0" --band="1/2 1/2 1/2 0 0 0 1/2 0 1/2"
  ```


