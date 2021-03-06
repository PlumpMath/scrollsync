# scrollsync

A reagent component for managing scroll events powered by core.async.

## Usage

[![Clojars Project](https://img.shields.io/clojars/v/scrollsync.svg)](https://clojars.org/scrollsync)

Scrollsync fires events based on the positioning of a collection of elements with respect to the browser window.

```clojure
(:require [reagent.core :as r]
          [scrollsync.core :refer [scrollsync])

(defn some-content
  []
  [:div
    [:div {:id "one"}
     [:p "lorem"]]
    [:div {:id "two"}
     [:p "ipsum"]]
    [:div {:id "three"}
     [:p "dolor"]]])

(defn my-scrollsync-view
  []
  [scrollsync :bp-fn       #(.log js/console %)
              :content     some-content
              :breakpoints [{:id "one"
                             :params "lorem!!!"
                             :break-at 100}
                            {:id "two"
                             :params "ipsum!!!"
                             :break-at 150}
                            {:id "three"
                             :params "dolor!!!"
                             :break-at 75}]]
```

## Parameters

### :bp-fn

`fn`

The function fired when a breakpoint is reached.

### :breakpoints

`[{:id "some-id" :params {:a "b"} :break-at 100}...]`

A collection of maps describing each element with a scroll event.

#### :id

the element's id

#### :params

the data passed to `bp-fn` when the breakpoint is reached

#### :break-at

the offset at which the element's breakpoint is triggered (an offset of 0 would fire an event when the top of the element reaches the top of the viewport)

### :content
`component`

scrollsync's child element


Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
