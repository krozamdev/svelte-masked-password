<script>
  import InputMaskingPassword from "@krozamdev/svelte-masked-password";
  
  let password = "";
  let showPassword = false;

  const handlePasswordChange = (newPassword) => {
    password = newPassword;
    console.log("Password changed: ", password);
  };

  const toggleShowPassword = () => {
    showPassword = !showPassword;
  };
</script>

<main>
  
  <button on:click={toggleShowPassword}>
    {showPassword ? "Hide Password" : "Show Password"}
  </button>

  <InputMaskingPassword
    onChangeEvent={handlePasswordChange}
    maskCharacter="•"
    showPassword={showPassword}
    placeholder="Enter your password"
  />
</main>
