#############################################################################
# Source files of Common library

# Package CORE (files ordered by lexicographical order i.e. ease of search).
set( Common_Core_SOURCES
  mvdAbstractImageModel.cxx
  mvdAbstractLayerModel.cxx
  mvdAbstractModel.cxx
  mvdAbstractWorker.cxx
  mvdBackgroundTask.cxx
  mvdCore.cxx
  mvdDatasetDescriptor.cxx
  mvdDataStream.cxx
  mvdDatabaseConnection.cxx
  mvdDatabaseError.cxx
  mvdDatabaseModel.cxx
  mvdDatabaseQueries.cxx
  mvdDatasetModel.cxx
  mvdFilenameInterface.cxx
  mvdHistogramModel.cxx
  mvdI18nCoreApplication.cxx
  mvdImageImporter.cxx
  mvdImagePlacenameLoader.cxx
  mvdImageProperties.cxx
  mvdImageSettings.cxx
  mvdImageSettingsInterface.cxx
  #mvdModifiableInterface.cxx
  #mvdMyClass.cxx
  mvdProgressInterface.cxx
  mvdProcessObjectObserver.cxx
  mvdOverviewBuilder.cxx
  mvdQuicklookModel.cxx
  mvdSerializableInterface.cxx
  mvdStackedLayerModel.cxx
  mvdTextStream.cxx
  mvdTypes.cxx
  mvdVectorImageModel.cxx
  mvdVectorImageSettings.cxx
  mvdVisibleInterface.cxx
)

#############################################################################
# Qt's MOC header files for Common library (QObject derived classes).

# Package CORE (files ordered by lexicographical order i.e. ease of search).
set( Common_Core_HEADERS_MOC
  mvdAbstractImageModel.h
  mvdAbstractLayerModel.h
  mvdAbstractModel.h
  mvdAbstractWorker.h
  # mvdAlgorithm.h
  mvdBackgroundTask.h
  # mvdCore.h
  mvdDatabaseConnection.h
  # mvdDatabaseError.h
  mvdDatabaseModel.h
  mvdDatabaseQueries.h
  mvdDatasetDescriptor.h
  mvdDatasetModel.h
  mvdHistogramModel.h
  mvdI18nCoreApplication.h
  mvdImageImporter.h
  mvdImagePlacenameLoader.h
  # mvdImageProperties.h
  # mvdMath.h
  #mvdMyClass.h
  mvdOverviewBuilder.h
  mvdQuicklookModel.h
  mvdStackedLayerModel.h
  # mvdSystemError.h
  # mvdTypes.h
  mvdVectorImageModel.h
)

#############################################################################
# Includes
include_directories(
  ${Monteverdi_BINARY_DIR}
  #
  ${Monteverdi_SOURCE_DIR}/Code/Common
  #${Monteverdi_SOURCE_DIR}/Code/Common/Core
  #
  ${Monteverdi_BINARY_DIR}/Code/Common
  ${Monteverdi_BINARY_DIR}/Code/Common/Core
)

#############################################################################
# Qt4 wrapped files (meta-object generated).
qt4_wrap_cpp( Common_Core_SRC_MOC ${Common_Core_HEADERS_MOC} )

########################################################################
# Qt4 translations.

# Sources files to translate.
add_to_qt4_i18n_sources( 
  ${Common_Core_SOURCES}
)

#############################################################################
add_library(Monteverdi_Core
  ${Common_Core_SOURCES}
  ${Common_Core_SRC_MOC}
)

#############################################################################
target_link_libraries(Monteverdi_Core
  ${OTB_LIBRARIES}
  Qt4::QtCore
  Qt4::QtSql
  Qt4::QtXml
)

#############################################################################
set_target_properties(Monteverdi_Core
  PROPERTIES ${Monteverdi_LIBRARY_PROPERTIES}
)

#############################################################################
if( GENERATE_SQL )
  add_dependencies( Monteverdi_Core Monteverdi_Sql )
endif( GENERATE_SQL )

#############################################################################
# INSTALL Common application.
install(
  TARGETS Monteverdi_Core
  RUNTIME DESTINATION ${Monteverdi_INSTALL_BIN_DIR} COMPONENT Runtime
  LIBRARY DESTINATION ${Monteverdi_INSTALL_LIB_DIR} COMPONENT Runtime
  ARCHIVE DESTINATION ${Monteverdi_INSTALL_LIB_DIR} COMPONENT Development
)

#############################################################################
