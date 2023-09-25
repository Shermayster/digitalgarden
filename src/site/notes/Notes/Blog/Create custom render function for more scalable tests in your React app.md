---
{"dg-publish":true,"permalink":"/notes/blog/create-custom-render-function-for-more-scalable-tests-in-your-react-app/"}
---

# Create custom render function for more scalable tests in your React app

Any React application will have global providers with. It can be styles, state or translation.
Testing those things can be tricky. Adding them can break our tests. Here's why we should add a custom render function to our application.

The following is an example of a translation library. But it can be any configuration and you can add more layers in the future without breaking your tests.

<iframe
  src="https://codesandbox.io/embed/custom-testing-render-forked-t9zs6?fontsize=14&hidenavigation=1&theme=dark&view=editor"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="custom-testing-render (forked)"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>