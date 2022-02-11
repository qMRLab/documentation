User preferences
===============================================================================

You can customize certain qMRLab features according to your needs by modifying the ``usr/preferences.json`` file.

1. Default method selection
-------------------------------------------------------------------------------

.. note::
    Takes effect only in MATLAB with GUI.

The ``GUIDefault`` field determines which qMRLab module will be shown first in the method selection dropdown by default. For example: 

.. code-block:: json

   "GUIDefault": {
       "Method": "vfa_t1"
   }

2. Parallelization settings
-------------------------------------------------------------------------------

``FitParallelWheneverPossible`` selection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. note::
    Takes effect only in MATLAB if the parallel computing toolbox is available. The number of workers depends on
    the computational resources, as well as the MATLAB preferences.

This field configures qMRLab to execute fitting using multiple CPU cores when the ``Fit Data`` button is
clicked in the GUI or when the ``FitBIDS`` command is issued.

.. code-block:: json

   "FitParallelWheneverPossible": true,

If you would like to use parallelization only for certain (voxelwise) methods, you can use `ParFitData` function. For details:

.. code-block:: matlab

   help ParFitData

``ParFitData`` configurations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Configures the default behavior of `ParFitData` function.

.. note::
    Takes effect only in MATLAB if the parallel computing toolbox is available. Only the voxelwise models (e.g., ``inversion_recovery``)
    are affected. 

.. code-block:: json

   "ParFitData": {
		"AutosaveEnabled": 1,
		"AutosaveInterval": 5,
		"Granularity": 3,
		"RemoveTmpOnSuccess": 1
	}

Each option is explained below.

.. toggle::
   
   - ``AutosaveEnabled`` ``[on 1, off 0, default 1]``
   

   Save partial results when a batch is done processing or when the ``AutosaveInterval`` is reached.

   - ``AutosaveInterval`` ``[min 1, default 5]``

   If ``AutosaveEnabled`` is set to 1, this option determines the duration (in minutes) at which the outputs will be saved. Each CPU worker times its own process.

   - ``Granularity`` ``[min 2, max 5, default 3]``
   

   Determines how many data chunks will be created to parallelize the fitting.

   ``nChunks = nCores X Granularity.``

   - ``RemoveTmpOnSuccess`` ``[min 2, max 5, default 3]``

   Determines whether to remove ``ParFitTempResults`` folder after the execution finished successfully. For further details about ``ParFitData``:

   .. code-block:: matlab

      help ParFitData

3. Unit configurations
-------------------------------------------------------------------------------

qMRLab aims at collecting qMRI implementations from different labs under one umbrella. We keep the implementations as close as possible to their original form and avoid enforcing a particular scaling.

By configuring ``preferences.json``, it is possible to unify the units across all qMRLab models. This high-level configuration framework gives users the flexibility to work with units they prefer and keep implementations closer to they were originally developed.
The units are handled for 3 main cases: 

- **Input protocol units:** Defines the units for the acquisition parameters (e.g., ``RepetitionTime`` in seconds or milliseconds).
- **Output map units:** Defines the units for the quantitative maps calculated by qMRLab (e.g., ``T1 map`` in seconds or milliseconds).
- **Input map units:** Some quantitative maps are provided as inputs to certain models. For example, a ``B1+ map`` can be provided for ``vfa_t1``, or a ``T1 map`` is expected by the ``mvf``. This category defines in which units does qMRLab expect a qMRI map as an input.

.. admonition:: Keywords for defining units in qMRLab
   :class: dropdown

   - Time
       - ``microsecond``
       - ``millisecond``
       - ``second``
       - ``minute``
       - ``hour``
   - Rate
       - ``reciprocal_microsecond``
       - ``reciprocal_millisecond``
       - ``reciprocal_second``
   - Fraction
       - ``fraction_decimal`` (from 0 to 1)
       - ``fraction_percent`` (from 0 to 100)
   - B1
       - ``relative_scaling_factor_decimal`` (-inf, 1=ideal, +inf)
       - ``relative_scaling_factor_percent`` (-inf, 100=ideal, +inf)
   - B0
       - ``offset_factor_hertz`` (-inf, 0Hz=ideal, +inf]
   - Susceptibility
       - ``part_per_million``
   - Angle
       - ``radian`` 
       - ``degree`` 
   - Diffusivity
       - ``square_meter_per_second``
       - ``square_micrometer_per_millisecond``
   - Arbitrary
       - ``arbitrary`` (not scaled)
   - Categorical
       - ``categorical`` (not scaled)
   - Length 
       - ``millimeter``
       - ``micrometer``
   - Tensor
       - ``tensor``

.. warning::
    To configure units in the ``preferences.json``, the units **MUST** be set using the unit keywords above. For example, to set ``Time`` unit to ms, the correct keyword is ``millisecond``, not ``ms`` or ``milliseconds``.

.. note::
    Unit changes take effect in both MATLAB and Octave. To see the unit changes in the GUI, you need to restart qMRLab after modifying the ``preferences.json`` file.

.. admonition:: The ``ForAllUnitsUseBIDS`` field
   :class: dropdown

    If this setting is ``true`` then:

    1. Output maps will be generated in BIDS units (for example, ``second`` for relaxometry outputs, or ``fraction_percent`` for fraction maps)
    2. Protocol values will be expected to be in BIDS units (for example,``second`` for ``RepetitionTime``)
    3. If a method inputs a fieldmap or quantitative map, they are expected to follow BIDS units (for example, ``relative_scaling_factor_percent`` for B1+ maps)

    .. code-block:: json

      "ForAllUnitsUseBIDS": true,

    .. warning::
        Setting this to ``true`` will override ``UnifyOutputMapUnits``, ``UnifyInputProtocolUnits`` and ``ChangeProvidedInputMapUnits``.

.. admonition:: The ``UnifyOutputMapUnits`` field
   :class: dropdown

    If ``"Enabled": true``, then the units defined for each unit category will determine 
    output units of the quantitative maps generated by qMRLab.

    .. code-block:: json

        "UnifyOutputMapUnits": {
             "Enabled": true,
             "Time": "second",
             ...
             }

    For example, if you set ``"Time": "millisecond",`` as shown above, all the time-relevant output maps (e.g., ``T1map``, ``T2map``) will be saved
    in milliseconds.

    For available units and unit categories, please see the list above.

    .. note::
        Overriden by ``ForAllUnitsUseBIDS (true)`` user setting or ``setenv('ISBIDS','1')`` environment variable.

.. admonition:: The ``UnifyInputProtocolUnits`` field
   :class: dropdown

    If ``"Enabled": true``, then the units defined for each unit category will determine 
    in which units are the inputs protocols expected.

    .. code-block:: json

    "UnifyInputProtocolUnits ": {
            "Enabled": true,
            "Time": "second",
            ...
            }

    For example, if you set ``"Time": "millisecond",`` as shown above, all the time-relevant protocols (e.g., ``EchoTime``, ``InversionTime``) will be expected
    in milliseconds.

    Activating this setting will change the protocol field labels in GUI and the units shown in demo scripts 
    generated by the ``qMRGenBatch`` function.

    For available units and unit categories, please see the list above.

    .. note::
        Overriden by ``ForAllUnitsUseBIDS (true)`` user setting or ``setenv('ISBIDS','1')`` environment variable.

.. admonition:: The ``ChangeProvidedInputMapUnits`` field
   :class: dropdown

    If ``"Enabled": true``, then the units defined for each unit category will determine 
    in which units are the input maps expected (e.g. ``B1+map`` or ``R1map``). 

    .. code-block:: json

    "ChangeProvidedInputMapUnits": {
        "Enabled": false,
        "Time": "second",
        "B1": "relative_scaling_factor_decimal",
        ...
        }

    For example, if you set ``B1`` as shown above, qMRLab will assume that the B1+ maps you provide are normalized such that ``1`` indicates ``actual`` = ``nominal`` flip angle. Values smaller than ``1`` will
    scale down the actual Flip Angle, and vice versa. Or, a ``T1map`` that is input to a qMRLab model (e.g., `mvf`) will be expected in the unit of seconds. 

    For available units and unit categories, please see the list above.

    .. note::
        Overriden by ``ForAllUnitsUseBIDS (true)`` user setting or ``setenv('ISBIDS','1')`` environment variable.

.. note::

    qMRLab will use the units provided by original implementations when all the following settings are disabled: 
    ``UnifyOutputMapUnits``, ``UnifyInputProtocolUnits``, ``ChangeProvidedInputMapUnits`` and ``ForAllUnitsUseBIDS``.

    In this case, different models may operate in different units. For example, for ``inversion_recovery`` it is 
    ``milliseconds``, whereas for ``vfa_t1`` it is seconds. 