
.. xfunction:: datatable.rowlast
    :src: src/core/expr/fnary/rowfirstlast.cc FExpr_RowFirstLast<FIRST>::apply_function
    :tests: tests/ijby/test-rowwise.py
    :cvar: doc_dt_rowlast
    :signature: rowlast(*cols)

    For each row, find the last non-missing value in `cols`. If all values
    in a row are missing, then this function will also produce a missing value.


    Parameters
    ----------
    cols: Expr
        Input columns.

    return: Expr
        f-expression consisting of one column and the same number
        of rows as in `cols`.

    except: TypeError
        The exception is raised when input columns have incompatible types.


    Examples
    --------
    ::

        >>> from datatable import dt, f
        >>> DT = dt.Frame({"A": [1, 1, 2, 1, 2],
        ...                "B": [None, 2, 3, 4, None],
        ...                "C":[True, False, False, True, True]})
        >>> DT
           |     A      B      C
           | int32  int32  bool8
        -- + -----  -----  -----
         0 |     1     NA      1
         1 |     1      2      0
         2 |     2      3      0
         3 |     1      4      1
         4 |     2     NA      1
        [5 rows x 3 columns]

    ::

        >>> DT[:, dt.rowlast(f[:])]
           |    C0
           | int32
        -- + -----
         0 |     1
         1 |     0
         2 |     0
         3 |     1
         4 |     1
        [5 rows x 1 column]

    ::

        >>> DT[[1, 3], 'C'] = None
        >>> DT
           |     A      B      C
           | int32  int32  bool8
        -- + -----  -----  -----
         0 |     1     NA      1
         1 |     1      2     NA
         2 |     2      3      0
         3 |     1      4     NA
         4 |     2     NA      1
        [5 rows x 3 columns]

    ::

        >>> DT[:, dt.rowlast(f[:])]
           |    C0
           | int32
        -- + -----
         0 |     1
         1 |     2
         2 |     0
         3 |     4
         4 |     1
        [5 rows x 1 column]


    See Also
    --------
    - :func:`rowfirst()` -- find the first non-missing value row-wise.
