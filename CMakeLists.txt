cmake_minimum_required(VERSION 3.9)

# Specify the tex file name
set(TEX_NAME mathematics)

# Define a LaTeX project, and specify where to find the UseLATEX commands
project(mathematics NONE)  # the NONE option has to be included, since we are not using the langue c, cxx, or Fortran
include(cmake/UseLATEX.cmake)  # I like anti-cluttering by moving the UseLATEX.cmake file into a separate directory


# BUILD: Add a file to the specified project
add_latex_document(${TEX_NAME}.tex BIBFILES ../../../../../Archief/Bibliotheek/library.bib
                   INPUTS
                        config/commands.tex
                        config/packages.tex
                        main/algebraic_structures.tex
                        main/algebras.tex
                        main/commutators.tex
                        main/calculus.tex
                        main/functions.tex
                        main/linear_maps.tex
                        main/linear_variation_method.tex
                        main/matrix.tex
                        main/misc.tex
                        main/morphisms.tex
                        main/representation_theory.tex
                        main/scalar_numerical_optimization.tex
                        main/symmetric_eigenvalue_problem.tex
                        main/systems_of_equations.tex
                    IMAGE_DIRS
                        images
                    )


# POST-BUILD: move the created .pdf-file to the pdf directory (copy and delete)
add_custom_command(TARGET "${TEX_NAME}_pdf" POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ${CMAKE_SOURCE_DIR}/pdf/"${TEX_NAME}.pdf"
    COMMAND ${CMAKE_COMMAND} -E remove "${TEX_NAME}.pdf"
    COMMENT "Moving PDF-file to pdf directory."
)
