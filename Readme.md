This package exports one function, Fit. It takes an arbitrary value and a
pointer, then tries to fit the value into the pointer as best it can.

    type T struct {
        I int
        S string
        T *T
    }

    var t T
    Fit([]interface{}{int64(1), []byte("foo"), nil}, &t)

    fmt.Println(t)

Currently, Fit can only deal with a handful of input types: int64, uint64,
[]byte, nil, and []interface{}. It should be expanded to handle any type.

It fits slices into structs by recursively fitting each element of the slice
to each field in the struct.

Fit returns an os.Error if it cannot get the data into the slot, for instance,
if the types are incompatible, if a numeric type overflows the slot, or if the
slot holds a fixed number of elements (i.e. it is an array or a struct) and
the input slice does not have the same number of elements.
