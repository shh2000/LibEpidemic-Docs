SEPIAR Model
=====

Strcture
------------

The strcture of SEPIAR model can be seen at **NPI/SEPIAR_graph.py**.

.. code-block:: python

    def get_eqs():
        graph = Graph('SEPIIsR', 'S')
        vertical_divide(graph, 'S', ['E', 'P', 'I', 'R'])
        horizontal_divide(graph, 'I', ['A'])
        vertical_divide(graph, 'I', ['Is'])
        horizontal_divide(graph, 'Is', ['Is_ct'])
        graph.add_single_node('Income')
        add_path(graph, 'E', 'Is')
        add_path(graph, 'Income', 'I')
        add_path(graph, 'P', 'Is')
        model = Model('SEIR_eqs', graph)
        return model

Formula
----------------

The formula and default parameters of SEPIAR model can be seen at **NPI/base_NPI_model.py**.

.. code-block:: python

    def get_model(r0, hidden, infect, confirm, sym_ratio, ct_ratio, remove, income, contact_ratio, s0, i0):
        model = get_eqs()
        inf = 2147483647.0
        popu = s0 + i0

        set_path_exp(model, 'Income', 'I', 'income')
        set_path_parameters(model, 'Income', 'I', 'income', income)

        set_path_exp(model, 'S', 'E', 'betaI*I*S*n+betaP*P*S*n+betaasym*Is_ct*S*n+betaasym*A*S*n')
        set_path_parameters(model, 'S', 'E', 'betaI', 0.1 * r0)
        set_path_parameters(model, 'S', 'E', 'betaP', r0)
        set_path_parameters(model, 'S', 'E', 'betaasym', 0.2 * r0)
        set_path_parameters(model, 'S', 'E', 'n', 1.0 / popu)

        set_path_exp(model, 'E', 'P', 'gamma*E*nocontact')
        set_path_parameters(model, 'E', 'P', 'gamma', 1.0 / hidden)
        set_path_parameters(model, 'E', 'P', 'nocontact', 1.0 - contact_ratio)

        set_path_exp(model, 'E', 'Is', 'E*contact')
        set_path_parameters(model, 'E', 'Is', 'contact', contact_ratio)

        set_path_exp(model, 'P', 'I', 'alpha*P*sym*nocontact')
        set_path_parameters(model, 'P', 'I', 'alpha', 1.0 / infect)
        set_path_parameters(model, 'P', 'I', 'sym', sym_ratio)
        set_path_parameters(model, 'P', 'I', 'nocontact', 1.0 - contact_ratio)

        set_path_exp(model, 'P', 'A', 'alpha*P*asym*nocontact')
        set_path_parameters(model, 'P', 'A', 'alpha', 1.0 / infect)
        set_path_parameters(model, 'P', 'A', 'asym', 1.0 - sym_ratio)
        set_path_parameters(model, 'P', 'A', 'nocontact', 1.0 - contact_ratio)

        set_path_exp(model, 'P', 'Is', 'P*contact')
        set_path_parameters(model, 'P', 'Is', 'contact', contact_ratio)

        set_path_exp(model, 'I', 'Is', 'confirm*I*noct')
        set_path_parameters(model, 'I', 'Is', 'confirm', 1.0 / confirm)
        set_path_parameters(model, 'I', 'Is', 'noct', 1.0 - ct_ratio)

        set_path_exp(model, 'I', 'Is_ct', 'confirm*I*ct')
        set_path_parameters(model, 'I', 'Is_ct', 'confirm', 1.0 / confirm)
        set_path_parameters(model, 'I', 'Is_ct', 'ct', ct_ratio)

        set_path_exp(model, 'Is', 'R', 'remove*Is')
        set_path_parameters(model, 'Is', 'R', 'remove', 1.0 / remove)

        set_path_exp(model, 'Is_ct', 'R', 'remove_ct*Is_ct')
        set_path_parameters(model, 'Is_ct', 'R', 'remove_ct', 1.0 / remove)

        set_path_exp(model, 'A', 'R', 'remove_A*A')
        set_path_parameters(model, 'A', 'R', 'remove_A', 1.0 / remove)

        init_value = {'S': s0, 'E': 10.0 * i0, 'P': 3.0 * i0, 'I': i0, 'Is_ct': 0.0, 'Is': 0.0, 'A': 0.0, 'R': 0.0,
                    'Income': inf}
        init_compartment(model, init_value)
        return model
