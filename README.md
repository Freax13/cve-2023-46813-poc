# CVE-2023-46813 PoC

1. Apply the patches in the `host-patches` folder to the Linux host and QEMU.
2. Start an SEV-SNP VM.
3. Run the code in this repo and wait for the message "waiting for the hypervisor to change memory to MMIO".
4. Spam the `attack` command in QEMU several times.
5. Once the exploit detects that the type of some of its memory has been changed to MMIO it will use the vulnerability to swap out its credentials with those of the init tasks.

Successful exploitation will look like this:

![](./screenshot.png)

The exploit doesn't rely on any absolute kernel offsets but relies on the relative offsets of fields in the `struct task_struct` type. You might have to adjust those.
