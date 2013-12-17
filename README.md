# Om

A ClojureScript interface to Facebook's React.

## Example

```clj
(ns example
  (:require [om.core :as om :include-macros true]
            [om.dom :as dom :include-macros true]))

(defn widget [data]
  (om/component
    (dom/div nil "Hello world!")))

(om/root {} widget js/document.body)
```

## Using it

Om is pre-alpha software. You also need to clone ClojureScript from
master and install it via `script/build`. You can clone the Om repo
and install it locally with `lein install`.

For local development your [lein-cljsbuild](http://github.com/emezeske/lein-cljsbuild) settings should look something like
this:

```clj
:cljsbuild { 
  :builds [{:id "dev"
            :source-paths ["src"]
            :compiler {
              :output-to "main.js"
              :output-dir "out"
              :optimizations :none
              :source-map true
              :externs ["om/externs/react.js"]}}]}
```

Your local development markup should look something like the following:

```
<script src="http://fb.me/react-0.5.1.js"></script>
<script src="out/goog/base.js" type="text/javascript"></script>
<script src="app.js" type="text/javascript"></script>
<script type="text/javascript">goog.require("todomvc.app");</script>
```

For production your [lein-cljsbuild](http://github.com/emezeske/lein-cljsbuild) settings should look something
like this:

```clj
:cljsbuild { 
  :builds [{:id "release"
            :source-paths ["src"]
            :compiler {
              :output-to "app.js"
              :optimizations :advanced
              :pretty-print false
              :preamble ["om/react.min.js"]
              :externs ["om/externs/react.js"]
              :closure-warnings
              {:non-standard-jsdoc :off}}}]}
```

This will generate a single file `app.js`.
