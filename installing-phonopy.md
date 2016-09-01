Following [Download and install — Phonopy v.1.11.0](https://atztogo.github.io/phonopy/install.html)

1. Download the package from  [phonopy - Browse /phonopy/phonopy-1.10 at SourceForge.net](https://sourceforge.net/projects/phonopy/files/phonopy/phonopy-1.10/)
2. extract package
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
