---
{"dg-publish":true,"permalink":"/blog/create-custom-render-function-for-more-scalable-tests-in-your-react-app/"}
---


Any React application will have global providers with. It can be styles, state or translation.
Testing those things can be tricky. Adding them can break our test. What's why we should add custom render function to our application.

Here is an example with translation. But it can any configuration and you can more layers in future without breaking your tests.

<iframe
  src="https://codesandbox.io/embed/custom-testing-render-forked-t9zs6?fontsize=14&hidenavigation=1&theme=dark&view=editor"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="custom-testing-render (forked)"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>