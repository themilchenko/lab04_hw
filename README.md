## Laboratory work IV

`Цель работы`:
лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса Travis CI

### Ход выполнения `Tutorial`:

```sh
$ export GITHUB_USERNAME=themilchenko
$ export GITHUB_TOKEN=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
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
```

```sh
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
$ . scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2
$ rvm use 2.4.2 --default
$ gem install travis
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04
$ cd projects/lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04
```

```sh
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```sh
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
  EOF
```

```sh
$ cat >> .travis.yml <<EOF

addons:
apt:
sources:
- george-edison55-precise-backports
packages:
- cmake
- cmake-data
EOF
```

```sh
$ travis login --github-token ${GITHUB_TOKEN}
```

```sh
$ travis lint
```

```sh
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
```

```sh
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"
$ git push origin master
```

```sh
$ travis lint
$ travis accounts
$ travis sync
$ travis repos
$ travis enable
$ travis whatsup
$ travis branches
$ travis history
$ travis show
```

```sh
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

### Выполнение ДЗ

```sh
$ mkdir lab04_hw
$ cd lab04_hw

$ git clone https://github.com/themilchenko/lab03_hw.git .
$ git remote remove origin
$ git remote add origin https://github.com/themilchenko/lab04_hw.git

$ touch .travis.yml
$ nano .travis.yml

languahe: cpp

script:
- cmake -Hformatter_lib -Bformatter_lib/_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build formatter_lib/_build
- cmake -Hformatter_ex_lib -Bformatter_ex_lib/_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build formatter_ex_lib/_build
- cmake -Hhello_world_application -Bhello_world_application/_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build hello_world_application/_build
- cmake -Hsolver_application -Bsolver_application/_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build solver_application/_build



addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
      
 $ git add .
 $ git commit -m "added .travis.yml"
 $ git push origin master     
```
