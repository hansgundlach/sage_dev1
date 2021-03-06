Groupes finis, groupes abéliens
===============================

Sage permet de faire des calculs avec des groupes de permutation, des
groupes classiques finis (tels que  :math:`SU(n,q)`), des groupes finis
de matrices (avec vos propres générateurs) et des groupes abéliens (même
infinis). La plupart de ces fonctionalités est implémentée par une
interface vers GAP.

Par exemple, pour créer un groupe de permutation, il suffit de donner
une liste de générateurs, comme dans l'exemple suivant.

::

    sage: G = PermutationGroup(['(1,2,3)(4,5)', '(3,4)'])
    sage: G
    Permutation Group with generators [(3,4), (1,2,3)(4,5)]
    sage: G.order()
    120
    sage: G.is_abelian()
    False
    sage: G.derived_series()           # sortie plus ou moins aléatoire (random)
    [Permutation Group with generators [(1,2,3)(4,5), (3,4)],
     Permutation Group with generators [(1,5)(3,4), (1,5)(2,4), (1,3,5)]]
    sage: G.center()
    Subgroup of (Permutation Group with generators [(3,4), (1,2,3)(4,5)]) generated by [()]
    sage: G.random_element()           # sortie aléatoire (random)
    (1,5,3)(2,4)
    sage: print latex(G)
    \langle (3,4), (1,2,3)(4,5) \rangle

On peut obtenir la table des caractères (au format LaTeX) à partir de Sage :

::

    sage: G = PermutationGroup([[(1,2),(3,4)], [(1,2,3)]])
    sage: latex(G.character_table())
    \left(\begin{array}{rrrr}
    1 & 1 & 1 & 1 \\
    1 & -\zeta_{3} - 1 & \zeta_{3} & 1 \\
    1 & \zeta_{3} & -\zeta_{3} - 1 & 1 \\
    3 & 0 & 0 & -1
    \end{array}\right)

Sage inclut aussi les groupes classiques ou matriciels définis sur des
corps finis :

::

    sage: MS = MatrixSpace(GF(7), 2)
    sage: gens = [MS([[1,0],[-1,1]]),MS([[1,1],[0,1]])]
    sage: G = MatrixGroup(gens)
    sage: G.conjugacy_class_representatives()
    (
    [1 0]  [0 6]  [0 4]  [6 0]  [0 6]  [0 4]  [0 6]  [0 6]  [0 6]  [4 0]
    [0 1], [1 5], [5 5], [0 6], [1 2], [5 2], [1 0], [1 4], [1 3], [0 2],
    <BLANKLINE>
    [5 0]
    [0 3]
    )
    sage: G = Sp(4,GF(7))
    sage: G
    Symplectic Group of degree 4 over Finite Field of size 7
    sage: G.random_element()  # élément du groupe tiré au hasard (random)
    [5 5 5 1]
    [0 2 6 3]
    [5 0 1 0]
    [4 6 3 4]
    sage: G.order()
    276595200

On peut aussi effectuer des calculs dans des groupes abéliens (infinis
ou finis) :

::

    sage: F = AbelianGroup(5, [5,5,7,8,9], names='abcde')
    sage: (a, b, c, d, e) = F.gens()
    sage: d * b**2 * c**3
    b^2*c^3*d
    sage: F = AbelianGroup(3,[2]*3); F
    Multiplicative Abelian group isomorphic to C2 x C2 x C2
    sage: H = AbelianGroup([2,3], names="xy"); H
    Multiplicative Abelian group isomorphic to C2 x C3
    sage: AbelianGroup(5)
    Multiplicative Abelian group isomorphic to Z x Z x Z x Z x Z
    sage: AbelianGroup(5).order()
    +Infinity