.. title: Заметка по qemu, virtio 3d и virgl: оно работает на nvidia драйверах!
.. slug: zametka-po-qemu-virtio-3d-i-virgl
.. date: 2022-04-24 10:30:38 UTC+05:00
.. tags: QEMU, Коротко, 
.. category: Дневник
.. link: 
.. description: Заметка по qemu, virtio 3d и virgl: оно работает на nvidia драйверах!
.. type: text

Коротко, чтобы самому не забыть. В линукс-эмуляторе QEMU есть такая экспериментальная фича, как Virtio 3d, она же virgl: виртуальная opengl 3.1 видеокарта. К сожалению, документации по ней с гулькин нос.

`virtio-gpu: qemu 6.1.0 no longer enables virgl when using '-vga virtio' <https://gitlab.com/qemu-project/qemu/-/issues/586>`_

Все инструкции, что я нашёл в интернете, не упоминают этот досадный факт.

    '-device virtio-vga-gl' works, but isn't obvious.

Работает, но это не очевидно. А я думал, что совсем не работает с nvidia-видеокартами. А да, virt-manager на рекомендуемой конфигурации тоже нихрена не работает с этим. 

Пример действительно рабочей конфигурации QEMU, чтобы самому не забыть:

.. code::

    qemu-system-x86_64 -m 8192 -enable-kvm -M q35 -cpu host -smp 24,cores=12,sockets=2 -device virtio-vga-gl -display sdl,gl=on -usb -device usb-tablet -cdrom ubuntu-22.04-desktop-amd64.iso -hda ubuntu.qcow2
