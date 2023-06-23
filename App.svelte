<script>
  import schema from "./schema";

  let values = {};
  let errors = {};

  const handleSubmit = async () => {
    try {
      await schema.validate(values, { abortEarly: false });
      alert(JSON.stringify(values, null, 2));
      errors = {};
    } catch (err) {
      errors = err.inner.reduce((acc, err) => {
        return { ...acc, [err.path]: err.message };
      }, {});
    }
  };
</script>

<div class="container">
  <h1>Registration Form</h1>
  <form on:submit|preventDefault={handleSubmit}>
    <div>
      <input
        type="text"
        name="email"
        bind:value={values.email}
        placeholder="Email"
      />

      {#if errors.email}
        <span class="error">{errors.email}</span>
      {/if}
    </div>

    <div>
      <input
        type="password"
        name="password"
        bind:value={values.password}
        placeholder="Password"
      />

      {#if errors.password}
        <span class="error">{errors.password}</span>
      {/if}
    </div>
    <div>
      <input
        type="password"
        name="confirmPassword"
        bind:value={values.confirmPassword}
        placeholder="Confirm password"
      />

      {#if errors.confirmPassword}
        <span class="error">{errors.confirmPassword}</span>
      {/if}
    </div>

    <div>
      <select name="hobby" bind:value={values.hobby}>
        <option value="">Select a hobby</option>
        <option value="Eating">Eating</option>
        <option value="Reading">Reading</option>
        <option value="Sleeping">Sleeping</option>
      </select>
      {#if errors.hobby}
        <span class="error">{errors.hobby}</span>
      {/if}
    </div>

    <div>
      <label for="checkbox">Check this box</label>
      <input name="checkbox" type="checkbox" bind:checked={values.checkbox} />
      {#if errors.checkbox}
        <span class="error">{errors.checkbox}</span>
      {/if}
    </div>

    <div>
      <button type="submit">Register</button>
    </div>
  </form>
</div>

<style>
  .container {
    margin: 0 auto;
    width: 400px;
  }

  form div {
    margin-top: 1em;
  }

  :root {
    --primary-light: #a6f9d6;
    --primary: #3361ea;
    --primary-dark: #5382ce;
    --secondary: #1e2145;
    --white: #fff;
    --grey: #e6e6ff;
    --grey-dark: #6d7098;
    --red: #ff6b6b;
  }

  input,
  select {
    font-family: inherit;
    font-size: inherit;
    max-width: 400px;
    width: 100%;
    padding: 12px;
    box-sizing: border-box;
    border: 1px solid var(--grey);
    border-radius: 4px;
    transition: all 150ms ease;
    background: var(--white);
  }

  input:focus,
  select:focus {
    outline: none;
    box-shadow: 0 0 0 4px rgb(227, 227, 245);
    border-color: var(--grey);
  }

  input:disabled,
  select:disabled {
    color: #ccc;
  }

  button {
    color: #fff;
    background-color: var(--primary);
    border: none;
    text-transform: uppercase;
    letter-spacing: 1.8px;
    outline: none;
    border-radius: 4px;
    display: block;
    margin-top: 12px;
    line-height: 1.8;
    font-size: 12px;
    padding: 10px 18px;
    width: 100%;
    transition: all 150ms ease;
    cursor: pointer;
  }

  button:disabled {
    background-color: var(--grey);
  }

  button:focus:not(:disabled) {
    box-shadow: 0 0 0 4px var(--primary-light);
  }

  button:hover:not(:disabled) {
    background-color: var(--primary-dark);
  }

  .error {
    display: block;
    font-size: 12px;
    color: var(--red);
  }
</style>
