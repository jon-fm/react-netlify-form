# React Netlify Form

A drop-in all-in-one solution for getting Netlify Forms on React-based SSGs
(Gatsby, Next, etc..) including automatic honeypot protection 💯📝

## Premise

The `<NetlifyForm>` is a turn-key solution to enable your Gatsby, Next, etc. site
with Netlify forms without having to worry about all of the details. Manage your
form's state however you prefer (a simple method shown below) then pass the value
collection to the component and let it handle the rest.

## Example

Simple form usage (https://react-netlify-form.demo.jon.fm)
```jsx
import React, { useState } from "react"
import NetlifyForm from 'react-netlify-form'

const IndexPage = () => {

  // Post-Submit Navigate
  const postSubmit = () => {
    navigate('/hooray')
  }

  // Simple controlled form setup (Control your own state)
  const handleChange = e => setFormValues({ ...formValues, [e.target.name]: e.target.value })
  const [formValues, setFormValues] = useState({
    name: '',
    message: ''
  })

  return (
    <Layout>

      <NetlifyForm formName="Very Simple Form" formValues={formValues} postSubmit={postSubmit} >
        <div>
          Your Name: <input type="text" name="name" value={formValues.name} onChange={handleChange} required />
        </div>
        <div>
          Message: <textarea name="message" value={formValues.message} onChange={handleChange} required />
        </div>
        <div>
          <button type="submit">Send</button>
        </div>
      </NetlifyForm>

      <div>
        <Link to="/medium" >For a bit more complex form, click here</Link>
      </div>
      <div>
        <a href="https://github.com/jon-fm/react-netlify-form-demo/blob/master/src/pages/index.js">To see the code, click here!</a>
      </div>
    </Layout>
  )
}
```

---

  /* 

  - Automatic Honeypot ✅
  - Pull this form in and have a functioning, awesome Netlify form. Literally
    no other plumbing required.

  API: 
    formName
    formValues
    
  Optional:
    preSubmit (async ready, return true, else no-op)
    postSubmit (no return necessary)
    automaticHoneypot

  */

  // Complicated stuff to keep things well-hidden during runtime (and from bots)
  // but exposed for netlify build bots