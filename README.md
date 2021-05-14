# cmpe283_Assignment3

## Steps followed:

1.Working environment same as Assignment 2

2.Add the code to calculate total exit count for the exit number in ecx

Inside function vmx_handle_exit in linux/arch/x86/kvm/vmx/vmx.c

       Declare an array to count the total number of exits, and perform atomic increment for index exit_reason.basic
     
Inside function kvm_emulate_cpuid in linux/arch/x86/kvm/cupid.c

      -Create a new leaf eax=0x4ffffffe. 
      
      -Inside eax, store exit count for the exit number in ecx.
      
      -Assign 0 in eax,ebx,ecx and 0x4ffffffe in edx for exit reason values in ecx that are not defined in the SDM.
      
      -Assign 0 to eax,ebx,ecx,edx for exit reason values in ecx that are not enabled in KVM.
      
3. Build the code using
        
        make && make modules && make install && make modules-install
        
4.Create test program in the inner VM that runs the following command for values 0 to 68 present in ecx.

        cpuid -l 0x4ffffffe -1 -s <exit number value in ecx>
        
### Frequency of exits

        Number of exits increase at a stable rate.
        
### Exit count in a full VM boot

        approximately 2million

### Most frequent exit

        EPT Violation
        
### Least Frequent Exit

        MOV DR
        
        WBINVD
